# Resteo Api v1

## Généralités

### Version API et `base_url`
L'API resteo migre vers sa version `v1`. Tous les calls à la v1 se feront dorénavant sur la base_url: `https://resteo-rails-production.herokuapp.com/api/v1`

## Endpoints

Les endpoints concernés sont:

- `/stats?request_params` Principales statistiques
- `/basket_breakdowns?request_params` Statistiques de décomposition du ticket moyen
- `/events?request_params`Evénements
- `/weathers?request_params`Données météo
- `/competition?request_params`Stats de concurrences

Ces endpoints seront gérés en **GET** avec des params dans l'URL. A priori, tous ces endpoints accepteront les mêmes `request_params`. Néanmoins, chaque endpoint n'a pas besoin d'accepter ces nouveaux `request_params` avec le même niveau de priorité. `/stats` et `/basket_breakdowns` doivent fonctionner avec le nouveau jeu de `request_params` pour la nouvelle version de Resteo d'octobre (release `CPOCC`). Les autres endpoints peuvent rester identique à la v0. **Il faudra le préciser au front en revanche.**

## Request Params

### Généralités
Les `request_params` doivent permettre de décrire requête d'un tableau croisé dynamique en séparant les aspects temporels du reste des aspects data. Les paramètres utilisés seront:

- `refrence_date`: Date de référence
- `where_period`: Type de période d'observation demandé. A combiner avec la date de référence.
- `group_period`: Split de regroupement de la `where_period`
- `compare_period`: Type de période de comparaison
- `compare_shift`: Shift de la période de comparaison. A combiner avec la `compare_period`
- `with_growth`: Flag de présence des données de growth par rapport à la `compare_period`
- `where_data`: Filtres de colonnes data à appliquer
- `group_data`: Split de regroupement des data 

### `reference_date`
- Nature: Date de référence
- Format: `YYYYMMDD` **Ca vous embête si on s'affranchit des `-`? Je préconise plus loin d'utiliser des clés dates et je préfèrerais tout sous la forme YYYYMMDD**
- Mandatory: Yes. 

### `where_period`
- Nature: Type de période d'observation demandé.
- Format: String parmi `['iso_day', 'week', 'month', 'year']`
- Mandatory: Yes. 
`reference_date` et `where_period` décrivent intégralement la période d'analyse demandée, qu'on appelle ici la `reference_period`.

### `group_period`
- Nature: Split de regroupement de la `where_period`. On demande une `where_period='month'` avec un `group_period='week'` par exemple.
- Format: String parmi `['iso_day', 'week', 'month', 'year']`
- Mandatory: No.

**Notes**: Lorsqu'on cherche a voir les données pour une semaine donnée sans breakdown par jour, on aura bien juste un `where_period=week` et **pas de `group_period`.**

### `compare_period`
- Nature: Type de période de comparaison.
- Format: String parmi `['year', 'where_period']`. Pour la release `CPOCC`, on aura toujours `year`.
- Mandatory: No.

### `compare_shift`
- Nature: Shift de la période de comparaison
- Format: Entier relatif. En release `CPOCC`, on aura toujours `compare_shift=-1`  et `compare_period='year'`. Autrement dit, on fera toujours de la comparaison par rapport à l'année dernière.
- Mandatory: No

### `with_growth`
- Nature: Flag de présence des données de growth par rapport à la `compare_period`
- Format: Boolean. Si `true`, les données de croissance entre la `reference_period` et la `comare_period` sont fournies dans la payload.
- Mandatory: No

### `where_data`
- Nature: Filtres de colonnes data à appliquer
- Format: Object dont les keys sont +/- les noms de colonnes de la DB et les values des lists de valeurs possibles. Clés possibles:
	````
	{
		restaurant_ids: [1, 2, 3, ],
		serving_types: ['lunch', 'dinner'],
		day_types: ['week', 'weekend'],
		consumption_place_type: ['onsite', 'takeway', 'delivery']
	}
	````
	Si la clé n'est pas présente, cela veut dire qu'on souhaite avoir la donnée pour toutes les valeurs de cette clé. Ainsi `where_data={servings_types:['lunch']}` signifie qu'on souhaite les stats **tout restaurant confondu**, c'est à dire les stats **total**, pour tout type de journée et tout type de `consumption_place`. A l'inverse `where_data={restaurant_ids:[2], serving_types:['lunch']}` , signifie que l'on souhaite les stats pour le restaurant_id 2 au déjeuner.
- Mandatory: No

### `group_data`
- Nature: Split de regroupement des data 
- Format: Liste de nom de colonnes de grouping. A priori, valeurs parmi les clés possibles pour la `where_data`: `['restaurant_ids', 'serving_types', 'day_types', 'consumption_place_type', 'waiters']`
- Mandatory: No

### Illustration Maquettes

Voir PJ des illustrations

## Réponses

### Généralités

Toutes les réponses contiendront une première clé request_params avec les params de la request.

### Nesting et keys

Les formes de payload sont à voir comme une vue ligne des données d'un TCD. La hiérarchie des clés de la data suit la hiérarchie de la requête des clés de `compare_period` puis de grouping, à savoir `group_period`, puis les clés associées aux `group_data`.

**Dans la mesure du possible, je préconise d'avoir des clés formées sur la date YYYYMMDD de début des périodes. Cela devrait nous permettre de passer plus de contexte assez simplement**. 

Pour une requête avec les request_params suivant (**! EN 2015 on a une semaine 53**):
````
request_params = {
	reference_date: '20161228',
	where_period: 'month',
	group_period: 'week',
	compared_period: 'year',
	compare_shift: -1,
	with_growth: true,
	group_data: ['restaurant_ids', 'day_types']
}
````
La réponse prendra la forme suivante
````
{
	message: {
		request_params: request_params,
		20160101: {
			20161128: { // week 48 en 2016
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20161205: { // week 49 en 2016
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20161212: { // week 50 en 2016
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20161219: { // week 51 en 2016
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20161226: { // week 52 en 2016
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
	    },
		20150101: {
			20151123: { // week 48 en 2015
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20151130: { // week 49 en 2015
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20151207: { // week 50 en 2015
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20151214: { // week 51 en 2015
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20151221: { // week 52 en 2015
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
			20151228: { // week 53 en 2015
				1 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
				2 :{
					week: { net_metrics },		
					weekend: { net_metrics }
				},
			},
	    },
		growth: {
			20161128: { // week 48 en 2016
				1 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
				2 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
			},
			20161205: { // week 49 en 2016
				1 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
				2 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
			},
			20161212: { // week 50 en 2016
				1 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
				2 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
			},
			20161219: { // week 51 en 2016
				1 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
				2 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
			},
			20161226: { // week 52 en 2016
				1 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
				2 :{
					week: { growth_to_date_metrics },		
					weekend: { growth_to_date_metrics }
				},
			},
	    },		
	},
	code: 200
}
````

**Remarques semaine 52/53/01:** 
- Avec des clés "fullcontext", `20181205` : le front peut plus facilement ordonner les clés dans le temps (`48, 49, 50, 51, 52, 01`; `53, 01, 02, 03, 04`). 
- Dans la réponse j'ai supposé que pour 2016 on sortait toutes les semaines de décembre 2016 (de 48 à 52), que pour 2015 on sortait toutes les semaines de décembre 2015 (de 49 à 53) et que pour la growth on sortait toutes les semaines de 2016 par rapport aux semaines de 2015, autrement dit de 48 à 52. **Est-ce vrai ?** Avec cette logique quand on demande du décembre 2015 (reference_date=20181224) par rapport à du 2014, on devrait avoir dans la clé growth les semaines 49 à 53 avec une des valeurs de growth égales à 0 pour la semaine 53. **Est-ce vrai ?**

### Absence de clé de grouping

**Les clés de grouping ne sont pas obligatoires dans les request_params et non obligatoire dans les payloads de réponse. On retrouvera des clés de grouping dans les payloads de réponse si les request_params en contenaient.** Typiquement pour les infos de synthèse sans breakdown répondant aux request_params suivant:
````
{
	reference_date: 20180328,
	where_period: 'month',
	compare_period: 'year',
	compare_shift: -1,
	with_growth: true,
	where_data: {restaurant_ids:[1]},
````
la réponse prendra la forme suivante:
````
{
	message: {
		request_params,
		20180101: {
			net_metrics
		}
		20170101: {
			net_metrics
		}
		growth: {
			growth_to_date_metrics
		}
	},
	code: 200
}
````
 
### net_metrics

Les net_metrics correspondent aux metrics métiers nets. Elles diffèrent selon les endpoints. Pour le endpoint `/stats `, elles correspondent essentiellement à total_sales, total_covers, average_cover et average_daily_sales. 
````
net_metrics = {
	calendar_start_date: 20180328, // start of the reference_period (-> reference_date * where_period)
	calendar_end_date: 20180328, // end of the reference_period (-> reference_date * where_period)
	data_start_date: 20180328, // first day taken into account for metrics calculation
	data_end_date: 20180328, // last day taken into account for metrics calculation
	days_count: 4, // number of days taken into account for metrics calculation
	total_sales: 4567,
	total_covers: 445,
	average_cover: 48,
	average_daily_sales: 480
}
````

### growth_to_date_metrics

Les growth_to_date_metrics correspondent aux points de croissance entre la reference_period (`reference_date * where_period`) et la `compare_period`. Elles s'expriment en % et se calculent à date. Elles diffèrent selon les endpoints. Pour le endpoint `/stats `, elles correspondent essentiellement à total_sales_growth, total_covers_growth, average_cover_growth et average_daily_sales_growth. 
````
growth_to_date_metrics = {
	calendar_start_date: 20180328, // start of the reference_period (-> reference_date * where_period)
	calendar_end_date: 20180328, // end of the reference_period (-> reference_date * where_period)
	data_start_date: 20180328, // first day taken into account for growth metrics calculation
	data_end_date: 20180328, // last day taken into account for growth metrics calculation
	days_count: 4, // number of days taken into account for growth metrics calculation
	total_sales_growth: 0.45,
	total_covers_growth: 0.23,
	average_cover_growth: 0.7,
	average_daily_sales_growth: 0.34
}
````

### Exemples

#### "Synthèse" Restaurant 1 Mars 2018
````
request_params = {
	reference_date: 20180328,
	where_period: 'month',
	compare_period: 'year',
	compare_shift: -1,
	with_growth: true,
	where_data: {restaurant_ids:[1]},
````
la réponse prendra la forme suivante:
````
{
	message: {
		request_params: {
			reference_date: 20180328,
			where_period: 'month',
			compare_period: 'year',
			compare_shift: -1,
			with_growth: true,
			where_data: {restaurant_ids:[1]},
		},
		20180101: {
			calendar_start_date: 20180322,
			calendar_end_date: 20180329,
			data_start_date: 20180322,
			data_end_date: 20180329,
			days_count: 4,
			total_sales: 4567,
			total_covers: 445,
			average_cover: 48,
			average_daily_sales: 480
		}
		20170101: {
			calendar_start_date: 20170320,
			calendar_end_date: 20170328,
			data_start_date: 20170323,
			data_end_date: 20170328,
			days_count: 3,
			total_sales: 3167,
			total_covers: 245,
			average_cover: 38,
			average_daily_sales: 480
		}
		growth: {
			calendar_start_date: 20180322,
			calendar_end_date: 20180329,
			data_start_date: 20180322,
			data_end_date: 20180329,
			days_count: 4,
			total_sales_growth: 0.45,
			total_covers_growth: 0.23,
			average_cover_growth: 0.7,
			average_daily_sales_growth: 0.34
		}
	},
	code: 200
}
````

#### "Synthèse" Multi Restaurant Mars 2018
````
request_params = {
	reference_date: 20180328,
	where_period: 'month',
	compare_period: 'year',
	compare_shift: -1,
	with_growth: true,
	group_data: ['restaurant_ids']
````
la réponse prendra la forme suivante:
````
{
	message: {
		request_params: {
			reference_date: 20180328,
			where_period: 'month',
			compare_period: 'year',
			compare_shift: -1,
			with_growth: true,
			group_data: ['restaurant_ids']
		},
		20180101: {
			1: {
				calendar_start_date: 20180320,
				calendar_end_date: 20180328,
				data_start_date: 20180323,
				data_end_date: 20180328,
				days_count: 3,
				total_sales: 3167,
				total_covers: 245,
				average_cover: 38,
				average_daily_sales: 480			
			},
			2: {
				calendar_start_date: 20180320,
				calendar_end_date: 20180328,
				data_start_date: 20180323,
				data_end_date: 20180328,
				days_count: 3,
				total_sales: 3167,
				total_covers: 245,
				average_cover: 38,
				average_daily_sales: 480			
			}
		}
		20170101: {
			1: {
				calendar_start_date: 20170320,
				calendar_end_date: 20170328,
				data_start_date: 20170323,
				data_end_date: 20170328,
				days_count: 3,
				total_sales: 3167,
				total_covers: 245,
				average_cover: 38,
				average_daily_sales: 480			
			},
			2: {
				calendar_start_date: 20170320,
				calendar_end_date: 20170328,
				data_start_date: 20170323,
				data_end_date: 20170328,
				days_count: 3,
				total_sales: 3167,
				total_covers: 245,
				average_cover: 38,
				average_daily_sales: 480			
			}
		}
		growth: {
			1: {
				calendar_start_date: 20170320,
				calendar_end_date: 20170328,
				data_start_date: 20170323,
				data_end_date: 20170328,
				days_count: 3,
				total_sales_growth: 0.45,
				total_covers_growth: 0.23,
				average_cover_growth: 0.7,
				average_daily_sales_growth: 0.34
			},
			2: {
				calendar_start_date: 20170320,
				calendar_end_date: 20170328,
				data_start_date: 20170323,
				data_end_date: 20170328,
				days_count: 3,
				total_sales_growth: 0.45,
				total_covers_growth: 0.23,
				average_cover_growth: 0.7,
				average_daily_sales_growth: 0.34
			}
		}
	},
	code: 200
}
````

#### Focus Restaurant 1 Mars 2018 par serving_types
````
request_params = {
	reference_date: 20180328,
	where_period: 'month',
	compare_period: 'year',
	compare_shift: -1,
	with_growth: true,
	where_data: {restaurant_ids:[1]},
	group_data: ['serving_types']
````
la réponse prendra la forme suivante:
````
{
	message: {
		request_params: {
			reference_date: 20180328,
			where_period: 'month',
			compare_period: 'year',
			compare_shift: -1,
			with_growth: true,
			where_data: {restaurant_ids:[1]},
			group_data: ['serving_types']
		},
		20180101: {
			lunch: {
				calendar_start_date: 20180320,
				calendar_end_date: 20180328,
				data_start_date: 20180323,
				data_end_date: 20180328,
				days_count: 3,
				total_sales: 3167,
				total_covers: 245,
				average_cover: 38,
				average_daily_sales: 480			
			},
			dinner: {
				calendar_start_date: 20180320,
				calendar_end_date: 20180328,
				data_start_date: 20180323,
				data_end_date: 20180328,
				days_count: 3,
				total_sales: 3167,
				total_covers: 245,
				average_cover: 38,
				average_daily_sales: 480			
			}
		}
		20170101: {
			lunch: {
				calendar_start_date: 20170320,
				calendar_end_date: 20170328,
				data_start_date: 20170323,
				data_end_date: 20170328,
				days_count: 3,
				total_sales: 3167,
				total_covers: 245,
				average_cover: 38,
				average_daily_sales: 480			
			},
			dinner: {
				calendar_start_date: 20170320,
				calendar_end_date: 20170328,
				data_start_date: 20170323,
				data_end_date: 20170328,
				days_count: 3,
				total_sales: 3167,
				total_covers: 245,
				average_cover: 38,
				average_daily_sales: 480			
			}
		}
		growth: {
			lunch: {
				calendar_start_date: 20170320,
				calendar_end_date: 20170328,
				data_start_date: 20170323,
				data_end_date: 20170328,
				days_count: 3,
				total_sales_growth: 0.45,
				total_covers_growth: 0.23,
				average_cover_growth: 0.7,
				average_daily_sales_growth: 0.34
			},
			dinner: {
				calendar_start_date: 20170320,
				calendar_end_date: 20170328,
				data_start_date: 20170323,
				data_end_date: 20170328,
				days_count: 3,
				total_sales_growth: 0.45,
				total_covers_growth: 0.23,
				average_cover_growth: 0.7,
				average_daily_sales_growth: 0.34
			}
		}
	},
	code: 200
}
````


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcyOTg1MzUxOCwtNDczNDU5NjA0LC0xMz
Y2MzAxNDE0LC02MTY2ODU5MTQsLTk0NDU5MDA2NiwtNTgzODAy
NjEzLDIwMTk3OTUwNTFdfQ==
-->