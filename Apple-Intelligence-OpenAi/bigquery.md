# BigQuery Client - Class BigQueryClient (1.36.0)

1.36.0 (latest) 1.35.2 1.34.7 1.33.1 1.32.0 1.31.1 1.30.3 1.29.0 1.28.3 1.27.0 1.26.1 1.25.1 1.24.2 1.23.10 Reference documentation and code samples for the BigQuery Client class BigQueryClient.

Google Cloud BigQuery allows you to create, manage, share and query data.

Find more information at the
[Google Cloud BigQuery Docs](https://cloud.google.com/bigquery/docs).

Example:

    use Google\Cloud\BigQuery\BigQueryClient;

    $bigQuery = new BigQueryClient();

## Namespace

Google \\ Cloud \\ BigQuery

## Methods

### __construct

Create a BigQuery client.

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `config` | `array` Configuration options. |
| `↳ apiEndpoint` | `string` The hostname with optional port to use in place of the default service endpoint. Example: `foobar.com` or `foobar.com:1234`. |
| `↳ projectId` | `string` The project ID from the Google Developer's Console. |
| `↳ authCache` | `CacheItemPoolInterface` A cache for storing access tokens. **Defaults to** a simple in memory implementation. |
| `↳ authCacheOptions` | `array` Cache configuration options. |
| `↳ authHttpHandler` | `callable` A handler used to deliver Psr7 requests specifically for authentication. |
| `↳ credentialsFetcher` | `FetchAuthTokenInterface` A credentials fetcher instance. |
| `↳ httpHandler` | `callable` A handler used to deliver Psr7 requests. Only valid for requests sent over REST. |
| `↳ keyFile` | `array` \[DEPRECATED\] This option is being deprecated because of a potential security risk. This option does not validate the credential configuration. The security risk occurs when a credential configuration is accepted from a source that is not under your control and used without validation on your side. If you know that you will be loading credential configurations of a specific type, it is recommended to create the credentials directly and configure them using the `credentialsFetcher` option instead. `use Google\Auth\Credentials\ServiceAccountCredentials; $credentialsFetcher = new ServiceAccountCredentials($scopes, $json); $creds = new BigQueryClient(['credentialsFetcher' => $creds]);` This will ensure that an unexpected credential type with potential for malicious intent is not loaded unintentionally. You might still have to do validation for certain credential types. If you are loading your credential configuration from an untrusted source and have not mitigated the risks (e.g. by validating the configuration yourself), make these changes as soon as possible to prevent security risks to your environment. Regardless of the method used, it is always your responsibility to validate configurations received from external sources. @see <https://cloud.google.com/docs/authentication/external/externally-sourced-credentials> |
| `↳ keyFilePath` | `string` \[DEPRECATED\] This option is being deprecated because of a potential security risk. This option does not validate the credential configuration. The security risk occurs when a credential configuration is accepted from a source that is not under your control and used without validation on your side. If you know that you will be loading credential configurations of a specific type, it is recommended to create the credentials directly and configure them using the `credentialsFetcher` option instead. `use Google\Auth\Credentials\ServiceAccountCredentials; $credentialsFetcher = new ServiceAccountCredentials($scopes, $json); $creds = new BigQueryClient(['credentialsFetcher' => $creds]);` This will ensure that an unexpected credential type with potential for malicious intent is not loaded unintentionally. You might still have to do validation for certain credential types. If you are loading your credential configuration from an untrusted source and have not mitigated the risks (e.g. by validating the configuration yourself), make these changes as soon as possible to prevent security risks to your environment. Regardless of the method used, it is always your responsibility to validate configurations received from external sources. @see <https://cloud.google.com/docs/authentication/external/externally-sourced-credentials> |
| `↳ requestTimeout` | `float` Seconds to wait before timing out the request. **Defaults to** `0` with REST and `60` with gRPC. |
| `↳ retries` | `int` Number of retries for a failed request. **Defaults to** `3`. |
| `↳ scopes` | `array` Scopes to be used for the request. |
| `↳ quotaProject` | `string` Specifies a user project to bill for access charges associated with the request. |
| `↳ returnInt64AsObject` | `bool` If true, 64 bit integers will be returned as a [Google\\Cloud\\Core\\Int64](https://docs.cloud.google.com/php/docs/reference/cloud-core/latest/Int64.html) object for 32 bit platform compatibility. **Defaults to** false. |
| `↳ location` | `string` If provided, determines the default geographic location used when creating datasets and managing jobs. Please note: This is only required for jobs started outside of the US and EU regions. Also, if location metadata has already been fetched over the network it will take precedent over this setting (by calling [Table::reload()](https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Table#_Google_Cloud_BigQuery_Table__reload__), for example). |
| `↳ logger` | `false|LoggerInterface` A PSR-3 compliant logger. If set to false, logging is disabled, ignoring the 'GOOGLE_SDK_PHP_LOGGING' environment flag |

### query

Returns a BigQuery job configuration.

The job configuration is passed to either
[BigQueryClient::runQuery()](https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/BigQueryClient#_Google_Cloud_BigQuery_BigQueryClient__runQuery__) or
[BigQueryClient::startQuery()](https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/BigQueryClient#_Google_Cloud_BigQuery_BigQueryClient__startQuery__). A
configuration can be built using fluent setters or by providing a full
set of options at once.

Unless otherwise specified, all configuration options will default based on the
[query job configuration](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery)
except for `configuration.query.useLegacySql`, which defaults to `false`
in this client.

Example:

    $queryJobConfig = $bigQuery->query(
        'SELECT commit FROM `bigquery-public-data.github_repos.commits` LIMIT 100'
    );

    // Set create disposition using fluent setters.
    $queryJobConfig = $bigQuery->query(
        'SELECT commit FROM `bigquery-public-data.github_repos.commits` LIMIT 100'
    )->createDisposition('CREATE_NEVER');

    // This is equivalent to the above example, using array configuration
    // instead of fluent setters.
    $queryJobConfig = $bigQuery->query(
        'SELECT commit FROM `bigquery-public-data.github_repos.commits` LIMIT 100',
        [
            'configuration' => [
                'query' => [
                    'createDisposition' => 'CREATE_NEVER'
                ]
            ]
        ]
    );

    // Set a region to run the job in.
    $queryJobConfig = $bigQuery->query(
        'SELECT name FROM `my_project.users_dataset.users` LIMIT 100'
    )->location('asia-northeast1');

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `query` | `string` A BigQuery SQL query. |
| `options` | `array` Configuration options. |
| `↳ configuration` | `array` Job configuration. Please see the [API documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfiguration) for the available options. | **Properties** || |---|---| | **Name** | **Description** | | `query` | `array` Query job configuration. Please see the [documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery) for the available options. | |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/QueryJobConfiguration` |   |

### queryConfig

Returns a BigQuery job configuration.

The job configuration is passed to either
[BigQueryClient::runQuery()](https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/BigQueryClient#_Google_Cloud_BigQuery_BigQueryClient__runQuery__) or
[BigQueryClient::startQuery()](https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/BigQueryClient#_Google_Cloud_BigQuery_BigQueryClient__startQuery__). A
configuration can be built using fluent setters or by providing a full
set of options at once.

Unless otherwise specified, all configuration options will default based on the
[query job configuration](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery)
except for `configuration.query.useLegacySql`, which defaults to `false`
in this client.

As this method is an alias, please see
[BigQueryClient::query()](https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/BigQueryClient#_Google_Cloud_BigQuery_BigQueryClient__query__) for usage examples.

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `query` | `string` A BigQuery SQL query. |
| `options` | `array` Configuration options. |
| `↳ configuration` | `array` Job configuration. Please see the [API documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfiguration) for the available options. | **Properties** || |---|---| | **Name** | **Description** | | `query` | `array` Query job configuration. Please see the [documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery) for the available options. | |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/QueryJobConfiguration` |   |

### runQuery

See also:

- [Jobs insert API Documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `query` | `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/QueryJobConfiguration` A BigQuery SQL query configuration. |
| `options` | `array` Configuration options. |
| `↳ maxResults` | `int` The maximum number of rows to return per page of results. Setting this flag to a small value such as 1000 and then paging through results might improve reliability when the query result set is large. |
| `↳ startIndex` | `int` Zero-based index of the starting row. |
| `↳ timeoutMs` | `int` How long, in milliseconds, each API call will wait for query results to become available before timing out. Depending on whether the $maxRetries has been exceeded, the results will be polled again after the timeout has been reached. **Defaults to** `10000` milliseconds (10 seconds). |
| `↳ maxRetries` | `int` The number of times to poll the Job status, until the job is complete. By default, will poll indefinitely. |
| `↳ returnRawResults` | `bool` Returns the raw data types returned from BigQuery without converting their values into native PHP types or the custom type classes supported by this library. Default is false. |
| `↳ formatOptions.useInt64Timestamp` | `boolean` Optional. Output timestamp as usec int64. Default is false. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/QueryResults` |   |

### startQuery

See also:

- [Jobs insert API documentation.](https://cloud.google.com/bigquery/docs/reference/v2/jobs/insert)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `query` | `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/QueryJobConfiguration` A BigQuery SQL query configuration. |
| `options` | `array` \[optional\] Configuration options. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Job` |   |

### job

Lazily instantiates a job.

There are no network requests made at this
point. To see the operations that can be performed on a job please
see [Job](https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Job).

Example:

    $job = $bigQuery->job('myJobId');

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `id` | `string` The id of the already run or running job to request. |
| `options` | `array` Configuration options. |
| `↳ location` | `string` The geographic location of the job. Required for jobs started outside of the US and EU regions. **Defaults to** a location specified in the client configuration. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Job` |   |

### jobs

See also:

- [Jobs list API documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/list)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `options` | `array` Configuration options. |
| `↳ allUsers` | `bool` Whether to display jobs owned by all users in the project. **Defaults to** `false`. |
| `↳ maxResults` | `int` Maximum number of results to return per page. |
| `↳ resultLimit` | `int` Limit the number of results returned in total. **Defaults to** `0` (return all results). |
| `↳ pageToken` | `string` A previously-returned page token used to resume the loading of results from a specific point. |
| `↳ stateFilter` | `string` Filter for job state. Maybe be either `done`, `pending`, or `running`. |
| `↳ maxCreationTime` | `int` Milliseconds since the POSIX epoch. If set, only jobs created before or at this timestamp are returned. |
| `↳ minCreationTime` | `int` Milliseconds since the POSIX epoch. If set, only jobs created after or at this timestamp are returned. |
| `↳ parentJobId` | `string` If set, show only child jobs of the specified parent. Otherwise, show all top-level jobs. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-core/latest/Iterator.ItemIterator.html<https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Job>` |   |

### dataset

Lazily instantiates a dataset.

There are no network requests made at this
point. To see the operations that can be performed on a dataset please
see [Dataset](https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Dataset).

If the dataset is owned by a different project than the project used to authenticate the client,
provide the project ID as the second argument.

Example:

    $dataset = $bigQuery->dataset('myDatasetId');

    // Reference a dataset from other project.
    $dataset = $bigQuery->dataset('samples', 'bigquery-public-data');

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `id` | `string` The id of the dataset to request. |
| `projectId` | `string|null` The id of the project. **Defaults to** current project id. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Dataset` |   |

### datasets

See also:

- [Datasets list API documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/list)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `options` | `array` Configuration options. |
| `↳ all` | `bool` Whether to list all datasets, including hidden ones. **Defaults to** `false`. |
| `↳ maxResults` | `int` Maximum number of results to return per page. |
| `↳ resultLimit` | `int` Limit the number of results returned in total. **Defaults to** `0` (return all results). |
| `↳ pageToken` | `string` A previously-returned page token used to resume the loading of results from a specific point. |
| `↳ filter` | `string` An expression for filtering the results of the request by label. The syntax is "labels. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-core/latest/Iterator.ItemIterator.html<https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Dataset>` |   |

### createDataset

See also:

- [Datasets insert API documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/insert)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `id` | `string` The id of the dataset to create. |
| `options` | `array` Configuration options. |
| `↳ accessPolicyVersion` | `int` Optional. Access policy schema version. Valid values are 0, 1, and 3. Requests specifying an invalid value will be rejected. Requests for conditional access policy binding in datasets must specify version 3. Dataset with no conditional role bindings in access policy may specify any valid value or leave the field unset. This field will be mapped to [IAM Policy version](https://cloud.google.com/iam/docs/policies#versions) and will be used to fetch policy from IAM. If unset or if 0 or 1 value is used for dataset with conditional bindings, access entry with condition will have role string appended by 'withcond' string followed by a hash value. For example : { "access": \[ { "role": "roles/bigquery.dataViewer_with_conditionalbinding_7a34awqsda", "userByEmail": "user@example.com", } \] } Please refer <https://cloud.google.com/iam/docs/troubleshooting-withcond> for more details. |
| `↳ metadata` | `array` The available options for metadata are outlined at the [Dataset Resource API docs](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets) |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Dataset` |   |

### runJob

See also:

- [Jobs insert API Documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `config` | `JobConfigurationInterface` The job configuration. |
| `options` | `array` Configuration options. |
| `↳ maxRetries` | `int` The number of times to retry, checking if the job has completed. **Defaults to** `100`. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Job` |   |

### startJob

See also:

- [Jobs insert API Documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `config` | `JobConfigurationInterface` The job configuration. |
| `options` | `array` \[optional\] Configuration options. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Job` |   |

### bytes

Create a Bytes object.

Example:

    $bytes = $bigQuery->bytes('hello world');

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `string|resource|Psr\Http\Message\StreamInterface` The bytes value. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Bytes` |   |

### date

Create a Date object.

Example:

    $date = $bigQuery->date(new \DateTime('1995-02-04'));

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `DateTimeInterface` The date value. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Date` |   |

### int64

Create an Int64 object. This can be used to work with 64 bit integers as
a string value while on a 32 bit platform.

Example:

    $int64 = $bigQuery->int64('9223372036854775807');

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `string` The 64 bit integer value in string format. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-core/latest/Int64.html` |   |

### time

Create a Time object.

Example:

    $time = $bigQuery->time(new \DateTime('12:15:00.482172'));

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `DateTimeInterface` The time value. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Time` |   |

### timestamp

Create a Timestamp object.

Example:

    $timestamp = $bigQuery->timestamp(new \DateTime('2003-02-05 11:15:02.421827Z'));

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `DateTimeInterface` The timestamp value. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Timestamp` |   |

### numeric

Create a Numeric object.

Numeric represents a value with a data type of
[Numeric](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#numeric_type).

It supports a fixed 38 decimal digits of precision and 9 decimal digits of scale, and values
are in the range of -99999999999999999999999999999.999999999 to
99999999999999999999999999999.999999999.

Example:

    $numeric = $bigQuery->numeric('99999999999999999999999999999999999999.999999999');

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `string|int|float` The Numeric value. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `numeric` |   |

### bigNumeric

Create a BigNumeric object.

Numeric represents a value with a data type of
[BIGNUMERIC](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#numeric_type).

It supports 76.76 (the 77th digit is partial) decimal digits of precision
and 38 decimal digits of scale. Values are in the range of
-5.7896044618658097711785492504343953926634992332820282019728792003956564819968E+38
to 5.7896044618658097711785492504343953926634992332820282019728792003956564819967E+38.

Example:

    $bigNumeric = $bigQuery->bigNumeric('999999999999999999999999999999999999999999999.99999999999999');

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `string|int|float` The Numeric value. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/BigNumeric` |   |

### geography

Create a Geography object.

Example:

    $geography = $bigQuery->geography('POINT(10 20)');

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `string` The geography data in WKT format. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Geography` |   |

### json

Create a BigQuery Json object.

Json represents a value with a data type of
[JSON](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#json_type)

Example:

    use Google\Cloud\BigQuery\BigQueryClient;

    $bigQuery = new BigQueryClient();
    $json = $bigQuery->json('{"key":"value"}');

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `value` | `string|null` The JSON string value. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/Json` |   |

### getServiceAccount

Get a service account for the KMS integration.

Example:

    $serviceAccount = $bigQuery->getServiceAccount();

| **Parameter** ||
|---|---|
| **Name** | **Description** |
| `options` | `array` \[optional\] Configuration options. |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `string` |   |

### copy

See also:

- [Jobs insert API Documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `options` | `array` Configuration options. |
| `↳ configuration` | `array` Job configuration. Please see the [API documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfiguration) for the available options. | **Properties** || |---|---| | **Name** | **Description** | | `copy` | `array` Copy job configuration. Please see the [documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationtablecopy) for the available options. | |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/CopyJobConfiguration` |   |

### extract

See also:

- [Jobs insert API Documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `options` | `array` Configuration options. |
| `↳ configuration` | `array` Job configuration. Please see the [API documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfiguration) for the available options. | **Properties** || |---|---| | **Name** | **Description** | | `extract` | `array` Extract job configuration. Please see the [documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationextract) for the available options. | |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/ExtractJobConfiguration` |   |

### load

See also:

- [Jobs insert API Documentation.](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert)

| **Parameters** ||
|---|---|
| **Name** | **Description** |
| `options` | `array` Configuration options. |
| `↳ configuration` | `array` Job configuration. Please see the [API documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfiguration) for the available options. | **Properties** || |---|---| | **Name** | **Description** | | `load` | `array` Load job configuration. Please see the [documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationload) for the available options. | |

| **Returns** ||
|---|---|
| **Type** | **Description** |
| `https://docs.cloud.google.com/php/docs/reference/cloud-bigquery/latest/LoadJobConfiguration` |   |

## Constants

### VERSION

    Value: '1.36.0'

### MAX_DELAY_MICROSECONDS

    Value: 32000000

### SERVICE_NAME

    Value: 'bigquery'

### SCOPE

    Value: 'https://www.googleapis.com/auth/bigquery'

### INSERT_SCOPE

    Value: 'https://www.googleapis.com/auth/bigquery.insertdata'
