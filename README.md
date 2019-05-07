# ![LOGO](logo.png) ODN **flow**ground Connector

## Description

A generated **flow**ground connector for the ODN API (version 1.0.0).

Generated from: https://api.apis.guru/v2/specs/opendatanetwork.com/1.0.0/swagger.json<br/>
Generated at: 2019-05-07T17:43:25+03:00

## API Description

The Socrata OpenDataNetwork (ODN) REST API exposes public data, often continuosly updated and enhanced, from many thousands of public
government and non profit agencies.

Much of this data originating from independent sources is fused together to create new, and often
powerful, entity level data. The API, in addition to search and autosuggest capabilities for finding datasets,
enables data based comparisons across geographical regions such as states, counties, metropolitan areas,
cities and zip codes using highly vetted data providers such as US Census, BEA, HUD and others. Comparison data
is preformatted for easy and efficient display on a chart, graph or interactive map.

The API also exposes data organized by narrative style questions a human might ask. The questions can
be rapidly found using an autosuggest style index, and then used to directly access all data needed to
thoroughly and authoritatively answer the question. Retrieved data includes time series (temporally aligned),
tabular, map heavy (includes spatial boundaries), and auto generated unstructured descriptive text.

The ODN API does not duplicate API endpoints or services provided by public sector agencies, but rather,
returns context relevant pre-populated REST URLs, when appropriate, so the caller can access data
directly from the source.

The [open source](http://github.com/socrata/odn-backend) API powers [OpenDataNetwork.com](http://OpenDataNetwork.com), an [open source](http://github.com/socrata/opendatanetwork.com)
site; the site highlights myriad uses and provides API badges with contextually relevant API example
REST endpoints and documentation pointers.

Finally, we continuously add new dat sources which appear automatically in the API, so if your favorite data
source is not available, check back soon. You can also join us [HERE](http://www.opendatanetwork.com/join-open-data-network)
and receive updates or let us know which data sources you are most interested in.

## App Tokens

Registering for and including a [Socrata application token](https://dev.socrata.com/docs/app-tokens.html)
is _required_ for the ODN API. They can be passed either using the `app_token` parameter
or the `X-App-Token` HTTP header.

## Authorization

This API does not require authorization.

## Actions

### Find all available data for some entities

#### Input Parameters
* `entity_id` - _required_ - Comma separated list of entity IDs.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

### Get constraint permutations for entities

#### Input Parameters
* `variable` - _required_ - Full ID of the variable to retrieve.
* `entity_id` - _required_ - Comma separated list of entity IDs.
* `constraint` - _required_ - Constraint to use.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

### Create a map

#### Input Parameters
* `variable` - _required_ - A single variable ID.
* `entity_id` - _required_ - A comma separated list of entity IDs.
Entities must have the same type and represent geographical regions.
* `constraint` - _optional_ - Values must be specified for each constraint in the dataset.
For example, to generate map data for `demographics.population.count`,
you must specify a value for `year` by passing `year=2013`.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

### Get values for variables

#### Input Parameters
* `variable` - _required_ - Comma separated list of variable IDs.
Defaults to retrieving all variables.
It is also possible to pass in a topic such as
`demographics`, or a dataset such as `demographics.population`,
which would both be equivalent to specifying
`demographics.population.count` and `demographics.population.change`.
Note that only variables in the same dataset are allowed.
* `entity_id` - _optional_ - Comma separated list of entity IDs.
Defaults to retrieving all entities.
Note that since there is currently no results pagination,
retrieving values for all entities may produce incomplete results.
* `forecast` - _optional_ - Number of steps to forecast.
Must be an integer between 0 and 20.
Forecasts are produced using linear extrapolation
on the data. They are only available when retrieving
data for a single variable across many numerical
constraint options.

+ Default `0`
* `describe` - _optional_ - Whether or not to produce a description of the data.
Set to `true` to produce a description.
Descriptions are not available if no entities are specified.

+ Default `false`
* `format` - _optional_ - If format is set to `google`, the data frame will be formatted
as a [Google Visualizations data table](https://developers.google.com/chart/interactive/docs/reference#datatable-class).
If the format is not provided or invalid, then the frame
will be formatted normally.
    Possible values: google.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

### Get Entities

#### Input Parameters
* `entity_id` - _optional_ - ID of the entity.
* `entity_name` - _optional_ - Name of the entity.
* `entity_type` - _optional_ - Type of the entity.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

### Find the relatives of an entity

#### Input Parameters
* `relation` - _required_ - The type of relation to find.
    Possible values: parent, child, sibling, peer.
* `entity_id` - _required_ - ID of the target entity.
* `variable_id` - _optional_ - If this parameter is included, only entities with data for the given
variable will be returned. Note that this may cause the number of
entities returned to be less than the specified `limit`.
* `limit` - _optional_ - Maximum number of entities in each group.
Must be an integer from 1 to 1000.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

### Get datasets

#### Input Parameters
* `entity_id` - _optional_ - Entities to use in formulating the query.
* `dataset_id` - _optional_ - If included, the search terms of the dataset
will be used in the query.
* `limit` - _optional_ - Maximum number of results to return.
Must be an integer from 0 to 50000.
* `offset` - _optional_ - Number of results to skip.
Used for pagination.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

### Get questions

#### Input Parameters
* `query` - _required_ - String to search against.
* `limit` - _optional_ - Maximum number of results to return.
Must be an integer from 0 to 50000.
* `offset` - _optional_ - Number of results to skip.
Used for pagination.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

### Get suggestions

#### Input Parameters
* `type` - _required_ - Type of the object to find.
    Possible values: entity, category, publisher, dataset, question.
* `query` - _required_ - Query to match.
* `limit` - _optional_ - Maximum number of results to return.
Must be an integer from 0 to 100.
* `variable_id` - _optional_ - This parameter is only available when suggesting entities with `type=entity`.
If it is provided, suggestions will be filtered to include
only entities that have data for the given variable.

If the variable provided is invalid, no entities will be returned.

Note that this filtering will increase response time significantly,
so it should only be used when necessary.
* `app_token` - _optional_ - The [Socrata App Token](https://dev.socrata.com/docs/app-tokens.html) to be
used with your request. The `app_token` parameter is required if an app token is not passed via the `X-App-Token` HTTP header. Clients must [register for their own app tokens](https://dev.socrata.com/docs/app-tokens.html).

## License

**flow**ground :- Telekom iPaaS / opendatanetwork-com-connector<br/>
Copyright © 2019, [Deutsche Telekom AG](https://www.telekom.de)<br/>
contact: flowground@telekom.de

All files of this connector are licensed under the Apache 2.0 License. For details
see the file LICENSE on the toplevel directory.
