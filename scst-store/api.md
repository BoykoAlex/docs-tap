


# API details

See [API walkthrough](api_walkthrough.md) for a walkthrough and example.

## <a id='info'></a>Information

### <a id='methods'></a>Version

0.0.1

## <a id='con-nego'></a>Content negotiation

### <a id='uri-schemes'></a>URI Schemes
* http
* https

### <a id='consumes'></a>Consumes
* application/json

### <a id='produce'></a>Produces
* application/json

## <a id='all-endpoints'></a>All endpoints

###  <a id='images'></a>images

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| POST | /api/imageReport | [create image report](#create-image-report) | Create a new image report. Related packages and vulnerabilities are also created. |
| GET | /api/images | [get images](#get-images) | Search image by id or digest. |
| GET | /api/packages/{IDorName}/images | [get package images](#get-package-images) | List the images that contain the given package. |
| GET | /api/vulnerabilities/{CVEID}/images | [get vulnerability images](#get-vulnerability-images) | List the images that contain the given vulnerability. |



###  <a id='operations'></a>Operations

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| GET | /api/health | [health check](#health-check) |  |



###  <a id='packages'></a>Packages

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| GET | /api/images/{IDorDigest}/packages | [get image packages](#get-image-packages) | List the packages in an image. |
| GET | /api/packages | [get packages](#get-packages) | Search packages by id, name and/or version. |
| GET | /api/sources/{IDorRepoorSha}/packages | [get source packages](#get-source-packages) |  |
| GET | /api/sources/packages | [get source packages query](#get-source-packages-query) | List packages of the given source. |
| GET | /api/vulnerabilities/{CVEID}/packages | [get vulnerability packages](#get-vulnerability-packages) | List packages that contain the given CVE id. |



###  <a id='sources'></a>Sources

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| POST | /api/sourceReport | [create source report](#create-source-report) | Create a new source report. Related packages and vulnerabilities are also created. |
| GET | /api/packages/{IDorName}/sources | [get package sources](#get-package-sources) | List the sources containing the given package. |
| GET | /api/sources | [get sources](#get-sources) | Search for sources by ID, repository, commit sha and/or organization. |
| GET | /api/vulnerabilities/{CVEID}/sources | [get vulnerability sources](#get-vulnerability-sources) | List sources that contain the given vulnerability. |



###  <a id='vulnerabilities'></a>Vulnerabilities

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| GET | /api/images/{IDorDigest}/vulnerabilities | [get image vulnerabilities](#get-image-vulnerabilities) | List vulnerabilities from the given image. |
| GET | /api/packages/{IDorName}/vulnerabilities | [get package vulnerabilities](#get-package-vulnerabilities) | List vulnerabilities from the given package. |
| GET | /api/sources/{IDorRepoorSha}/vulnerabilities | [get source vulnerabilities](#get-source-vulnerabilities) |  |
| GET | /api/sources/vulnerabilities | [get source vulnerabilities query](#get-source-vulnerabilities-query) | List vulnerabilities of the given source. |
| GET | /api/vulnerabilities | [get vulnerabilities](#get-vulnerabilities) | Search for vulnerabilities by CVE id. |



## <a id='paths'></a>Paths

### <a id="create-image-report"></a> Create a new image report. Related packages and vulnerabilities are also created. (*CreateImageReport*)

```
POST /api/imageReport
```

#### <a id='parameters-cir'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| Image | `body` | [Image](#image) | `models.Image` | | ✓ | |  |

#### <a id='all-responses-cir'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#create-image-report-200) | OK | Image |  | [schema](#create-image-report-200-schema) |
| [default](#create-image-report-default) | | ErrorMessage |  | [schema](#create-image-report-default-schema) |

#### <a id='responses-cir'></a>Responses


##### <span id="create-image-report-200"></span> 200 - Image
Status: OK

###### <span id="create-image-report-200-schema"></span> Schema



[Image](#image)

##### <span id="create-image-report-default"></span> Default Response
ErrorMessage

###### <span id="create-image-report-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="create-source-report"></a> Create a new source report. Related packages and vulnerabilities are also created. (*CreateSourceReport*)

```
POST /api/sourceReport
```

#### <a id='parameters-csr'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| Image | `body` | [Source](#source) | `models.Source` | | ✓ | |  |

#### <a id='all-responses-csr'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#create-source-report-200) | OK | Source |  | [schema](#create-source-report-200-schema) |
| [default](#create-source-report-default) | | ErrorMessage |  | [schema](#create-source-report-default-schema) |

#### <a id='responses-csr'></a>Responses


##### <span id="create-source-report-200"></span> 200 - Source
Status: OK

###### <span id="create-source-report-200-schema"></span> Schema



[Source](#source)

##### <span id="create-source-report-default"></span> Default Response
ErrorMessage

###### <span id="create-source-report-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-image-packages"></a> List the packages in an image. (*GetImagePackages*)

```
GET /api/images/{IDorDigest}/packages
```

#### <a id='parameters-gip'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| IDorDigest | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gip'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-image-packages-200) | OK | Package |  | [schema](#get-image-packages-200-schema) |
| [default](#get-image-packages-default) | | ErrorMessage |  | [schema](#get-image-packages-default-schema) |

#### <a id='responses-gip'></a>Responses


##### <span id="get-image-packages-200"></span> 200 - Package
Status: OK

###### <span id="get-image-packages-200-schema"></span> Schema



[][Package](#package)

##### <span id="get-image-packages-default"></span> Default Response
ErrorMessage

###### <span id="get-image-packages-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-image-vulnerabilities"></a> List vulnerabilities from the given image. (*GetImageVulnerabilities*)

```
GET /api/images/{IDorDigest}/vulnerabilities
```

#### <a id='parameters-giv'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| IDorDigest | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-giv'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-image-vulnerabilities-200) | OK | Vulnerability |  | [schema](#get-image-vulnerabilities-200-schema) |
| [default](#get-image-vulnerabilities-default) | | ErrorMessage |  | [schema](#get-image-vulnerabilities-default-schema) |

#### <a id='responses-giv'></a>Responses


##### <span id="get-image-vulnerabilities-200"></span> 200 - Vulnerability
Status: OK

###### <span id="get-image-vulnerabilities-200-schema"></span> Schema



[][Vulnerability](#vulnerability)

##### <span id="get-image-vulnerabilities-default"></span> Default Response
ErrorMessage

###### <span id="get-image-vulnerabilities-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-images"></a> Search image by id or digest. (*GetImages*)

```
GET /api/images
```

#### <a id='parameters-gi'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| digest | `query` | string | `string` |  |  |  |  |
| id | `query` | int64 (formatted integer) | `int64` |  |  |  |  |

#### <a id='all-responses-GI'></a> responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-images-200) | OK | Image |  | [schema](#get-images-200-schema) |
| [default](#get-images-default) | | ErrorMessage |  | [schema](#get-images-default-schema) |

#### <a id='responses-gi'></a>Responses


##### <span id="get-images-200"></span> 200 - Image
Status: OK

###### <span id="get-images-200-schema"></span> Schema



[Image](#image)

##### <span id="get-images-default"></span> Default Response
ErrorMessage

###### <span id="get-images-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-package-images"></a> List the images that contain the given package. (*GetPackageImages*)

```
GET /api/packages/{IDorName}/images
```

#### <a id='parameters-gpi'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| IDorName | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses5'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-package-images-200) | OK | Image |  | [schema](#get-package-images-200-schema) |
| [default](#get-package-images-default) | | ErrorMessage |  | [schema](#get-package-images-default-schema) |

#### <a id='responses-gpi'></a>Responses


##### <span id="get-package-images-200"></span> 200 - Image
Status: OK

###### <span id="get-package-images-200-schema"></span> Schema



[][Image](#image)

##### <span id="get-package-images-default"></span> Default Response
ErrorMessage

###### <span id="get-package-images-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-package-sources"></a> List the sources containing the given package. (*GetPackageSources*)

```
GET /api/packages/{IDorName}/sources
```

#### <a id='parameters-gps'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| IDorName | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gps'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-package-sources-200) | OK | Source |  | [schema](#get-package-sources-200-schema) |
| [default](#get-package-sources-default) | | ErrorMessage |  | [schema](#get-package-sources-default-schema) |

#### <a id='responses-gps'></a>Responses


##### <span id="get-package-sources-200"></span> 200 - Source
Status: OK

###### <span id="get-package-sources-200-schema"></span> Schema



[][Source](#source)

##### <span id="get-package-sources-default"></span> Default Response
ErrorMessage

###### <span id="get-package-sources-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-package-vulnerabilities"></a> List vulnerabilities from the given package. (*GetPackageVulnerabilities*)

```
GET /api/packages/{IDorName}/vulnerabilities
```

#### <a id='parameters-gpv'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| IDorName | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gpv'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-package-vulnerabilities-200) | OK | Vulnerability |  | [schema](#get-package-vulnerabilities-200-schema) |
| [default](#get-package-vulnerabilities-default) | | ErrorMessage |  | [schema](#get-package-vulnerabilities-default-schema) |

#### <a id='responses-gpv'></a>Responses


##### <span id="get-package-vulnerabilities-200"></span> 200 - Vulnerability
Status: OK

###### <span id="get-package-vulnerabilities-200-schema"></span> Schema



[][Vulnerability](#vulnerability)

##### <span id="get-package-vulnerabilities-default"></span> Default Response
ErrorMessage

###### <span id="get-package-vulnerabilities-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-packages"></a> Search packages by id, name and/or version. (*GetPackages*)

```
GET /api/packages
```

#### <a id='parameters-gp'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `query` | int64 (formatted integer) | `int64` |  |  |  | Any of id or name must be provided |
| name | `query` | string | `string` |  |  |  | Any of id or name must be provided |
| version | `query` | string | `string` |  |  |  |  |

#### <a id='all-responses-gp'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-packages-200) | OK | Package |  | [schema](#get-packages-200-schema) |
| [default](#get-packages-default) | | ErrorMessage |  | [schema](#get-packages-default-schema) |

#### <a id='responses-gp'></a>Responses


##### <span id="get-packages-200"></span> 200 - Package
Status: OK

###### <span id="get-packages-200-schema"></span> Schema



[][Package](#package)

##### <span id="get-packages-default"></span> Default Response
ErrorMessage

###### <span id="get-packages-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-source-packages"></a> get source packages (*GetSourcePackages*)

```
GET /api/sources/{IDorRepoorSha}/packages
```

#### <a id='parameters-gsp'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| IDorRepoorSha | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gsp'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-source-packages-200) | OK | Package |  | [schema](#get-source-packages-200-schema) |
| [default](#get-source-packages-default) | | ErrorMessage |  | [schema](#get-source-packages-default-schema) |

#### <a id='responses-gsp'></a>Responses


##### <span id="get-source-packages-200"></span> 200 - Package
Status: OK

###### <span id="get-source-packages-200-schema"></span> Schema



[][Package](#package)

##### <span id="get-source-packages-default"></span> Default Response
ErrorMessage

###### <span id="get-source-packages-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-source-packages-query"></a> List packages of the given source. (*GetSourcePackagesQuery*)

```
GET /api/sources/packages
```

#### <a id='parameters-gspq'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `query` | uint64 (formatted integer) | `uint64` |  |  |  |  |
| repo | `query` | string | `string` |  |  |  |  |
| sha | `query` | string | `string` |  |  |  |  |

#### <a id='all-responses-gspq'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-source-packages-query-200) | OK | Package |  | [schema](#get-source-packages-query-200-schema) |
| [default](#get-source-packages-query-default) | | ErrorMessage |  | [schema](#get-source-packages-query-default-schema) |

#### <a id='responses-gspq'></a>Responses


##### <span id="get-source-packages-query-200"></span> 200 - Package
Status: OK

###### <span id="get-source-packages-query-200-schema"></span> Schema



[][Package](#package)

##### <span id="get-source-packages-query-default"></span> Default Response
ErrorMessage

###### <span id="get-source-packages-query-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-source-vulnerabilities"></a> get source vulnerabilities (*GetSourceVulnerabilities*)

```
GET /api/sources/{IDorRepoorSha}/vulnerabilities
```

#### <a id='parameters-gsv'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| IDorRepoorSha | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gsv'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-source-vulnerabilities-200) | OK | Vulnerability |  | [schema](#get-source-vulnerabilities-200-schema) |
| [default](#get-source-vulnerabilities-default) | | ErrorMessage |  | [schema](#get-source-vulnerabilities-default-schema) |

#### <a id='responses-gsv'></a>Responses


##### <span id="get-source-vulnerabilities-200"></span> 200 - Vulnerability
Status: OK

###### <span id="get-source-vulnerabilities-200-schema"></span> Schema



[][Vulnerability](#vulnerability)

##### <span id="get-source-vulnerabilities-default"></span> Default Response
ErrorMessage

###### <span id="get-source-vulnerabilities-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-source-vulnerabilities-query"></a> List vulnerabilities of the given source. (*GetSourceVulnerabilitiesQuery*)

```
GET /api/sources/vulnerabilities
```

#### <a id='parameters-gsvq'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `query` | uint64 (formatted integer) | `uint64` |  |  |  |  |
| repo | `query` | string | `string` |  |  |  |  |
| sha | `query` | string | `string` |  |  |  |  |

#### <a id='all-responses-gsvq'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-source-vulnerabilities-query-200) | OK | Vulnerability |  | [schema](#get-source-vulnerabilities-query-200-schema) |
| [default](#get-source-vulnerabilities-query-default) | | ErrorMessage |  | [schema](#get-source-vulnerabilities-query-default-schema) |

#### <a id='responses-gsvq'></a>Responses


##### <span id="get-source-vulnerabilities-query-200"></span> 200 - Vulnerability
Status: OK

###### <span id="get-source-vulnerabilities-query-200-schema"></span> Schema



[][Vulnerability](#vulnerability)

##### <span id="get-source-vulnerabilities-query-default"></span> Default Response
ErrorMessage

###### <span id="get-source-vulnerabilities-query-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-sourcs"></a> Search for sources by ID, repository, commit sha and/or organization. (*GetSourcs*)

```
GET /api/sources
```

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-sourcs-200) | OK | Source |  | [schema](#get-sourcs-200-schema) |
| [default](#get-sourcs-default) | | ErrorMessage |  | [schema](#get-sourcs-default-schema) |

#### Responses


##### <span id="get-sourcs-200"></span> 200 - Source
Status: OK

###### <span id="get-sourcs-200-schema"></span> Schema



[][Source](#source)

##### <span id="get-sourcs-default"></span> Default Response
ErrorMessage

###### <span id="get-sourcs-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-vulnerabilities"></a> Search for vulnerabilities by CVE id. (*GetVulnerabilities*)

```
GET /api/vulnerabilities
```

#### <a id='parameters-gv'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| CVEID | `query` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gv'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-vulnerabilities-200) | OK | Vulnerability |  | [schema](#get-vulnerabilities-200-schema) |
| [default](#get-vulnerabilities-default) | | ErrorMessage |  | [schema](#get-vulnerabilities-default-schema) |

#### <a id='responses-gv'></a>Responses


##### <span id="get-vulnerabilities-200"></span> 200 - Vulnerability
Status: OK

###### <span id="get-vulnerabilities-200-schema"></span> Schema



[][Vulnerability](#vulnerability)

##### <span id="get-vulnerabilities-default"></span> Default Response
ErrorMessage

###### <span id="get-vulnerabilities-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-vulnerability-images"></a> List the images that contain the given vulnerability. (*GetVulnerabilityImages*)

```
GET /api/vulnerabilities/{CVEID}/images
```

#### <a id='parameters-gvi'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| CVEID | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gvi'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-vulnerability-images-200) | OK | Image |  | [schema](#get-vulnerability-images-200-schema) |
| [default](#get-vulnerability-images-default) | | ErrorMessage |  | [schema](#get-vulnerability-images-default-schema) |

#### <a id='responses-gvi'></a>Responses


##### <span id="get-vulnerability-images-200"></span> 200 - Image
Status: OK

###### <span id="get-vulnerability-images-200-schema"></span> Schema



[][Image](#image)

##### <span id="get-vulnerability-images-default"></span> Default Response
ErrorMessage

###### <span id="get-vulnerability-images-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-vulnerability-packages"></a> List packages that contain the given CVE id. (*GetVulnerabilityPackages*)

```
GET /api/vulnerabilities/{CVEID}/packages
```

#### <a id='parameters-gvp'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| CVEID | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gvp'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-vulnerability-packages-200) | OK | Package |  | [schema](#get-vulnerability-packages-200-schema) |
| [default](#get-vulnerability-packages-default) | | ErrorMessage |  | [schema](#get-vulnerability-packages-default-schema) |

#### <a id='responses-gvp'></a>Responses


##### <span id="get-vulnerability-packages-200"></span> 200 - Package
Status: OK

###### <span id="get-vulnerability-packages-200-schema"></span> Schema



[][Package](#package)

##### <span id="get-vulnerability-packages-default"></span> Default Response
ErrorMessage

###### <span id="get-vulnerability-packages-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="get-vulnerability-sources"></a> List sources that contain the given vulnerability. (*GetVulnerabilitySources*)

```
GET /api/vulnerabilities/{CVEID}/sources
```

#### <a id='parameters-gvs'></a>Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| CVEID | `path` | string | `string` |  | ✓ |  |  |

#### <a id='all-responses-gvs'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-vulnerability-sources-200) | OK | Source |  | [schema](#get-vulnerability-sources-200-schema) |
| [default](#get-vulnerability-sources-default) | | ErrorMessage |  | [schema](#get-vulnerability-sources-default-schema) |

#### <a id='responses-gvs'></a>Responses


##### <span id="get-vulnerability-sources-200"></span> 200 - Source
Status: OK

###### <span id="get-vulnerability-sources-200-schema"></span> Schema



[][Source](#source)

##### <span id="get-vulnerability-sources-default"></span> Default Response
ErrorMessage

###### <span id="get-vulnerability-sources-default-schema"></span> Schema



[ErrorMessage](#error-message)

### <a id="health-check"></a> health check (*HealthCheck*)

```
GET /api/health
```

#### <a id='all-responses-hc'></a>All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#health-check-200) | OK |  |  | [schema](#health-check-200-schema) |
| [default](#health-check-default) | | ErrorMessage |  | [schema](#health-check-default-schema) |

#### <a id='parameters-hc'></a>Responses


##### <span id="health-check-200"></span> 200
Status: OK

###### <span id="health-check-200-schema"></span> Schema

##### <span id="health-check-default"></span> Default Response
ErrorMessage

###### <span id="health-check-default-schema"></span> Schema



[ErrorMessage](#error-message)

## Models

### <a id="deleted-at"></a> DeletedAt





* composed type [NullTime](#null-time)

### <a id="error-message"></a> ErrorMessage


> ErrorMessage wraps an error message in a struct so responses are properly
marshalled as a JSON object.






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| Message | string| `string` |  | | in: body | `something went wrong` |



### <a id="image"></a> Image






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| Digest | string| `string` | ✓ | |  | `9n38274ods897fmay487gsdyfga678wr82` |
| ID | uint64 (formatted integer)| `uint64` |  | |  |  |
| Name | string| `string` | ✓ | |  | `myorg/application` |
| Packages | [][Package](#package)| `[]*Package` |  | |  |  |
| Registry | string| `string` | ✓ | |  | `docker.io` |
| Sources | [][Source](#source)| `[]*Source` |  | |  |  |



### <a id="method-type"></a> MethodType






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| CreatedAt | date-time (formatted string)| `strfmt.DateTime` |  | |  |  |
| DeletedAt | [DeletedAt](#deleted-at)| `DeletedAt` |  | |  |  |
| ID | uint64 (formatted integer)| `uint64` |  | |  |  |
| Name | string| `string` |  | |  |  |
| Rating | [][Rating](#rating)| `[]*Rating` |  | |  |  |
| UpdatedAt | date-time (formatted string)| `strfmt.DateTime` |  | |  |  |



### <a id="model"></a> Model


> Model a basic GoLang struct which includes the following fields: ID, CreatedAt, UpdatedAt, DeletedAt
It may be embedded into your model or you may build your own model without it
type User struct {
gorm.Model
}






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| CreatedAt | date-time (formatted string)| `strfmt.DateTime` |  | |  |  |
| DeletedAt | [DeletedAt](#deleted-at)| `DeletedAt` |  | |  |  |
| ID | uint64 (formatted integer)| `uint64` |  | |  |  |
| UpdatedAt | date-time (formatted string)| `strfmt.DateTime` |  | |  |  |



### <a id="null-time"></a> NullTime


> NullTime implements the Scanner interface so
it can be used as a scan destination, similar to NullString.






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| Time | date-time (formatted string)| `strfmt.DateTime` |  | |  |  |
| Valid | boolean| `bool` |  | |  |  |



### <a id="package"></a> Package






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| Homepage | string| `string` |  | |  |  |
| ID | uint64 (formatted integer)| `uint64` |  | |  |  |
| Images | [][Image](#image)| `[]*Image` |  | |  |  |
| Name | string| `string` |  | |  |  |
| PackageManager | string| `string` |  | |  |  |
| Sources | [][Source](#source)| `[]*Source` |  | |  |  |
| Version | string| `string` |  | |  |  |
| Vulnerabilities | [][Vulnerability](#vulnerability)| `[]*Vulnerability` |  | |  |  |



### <a id="rating"></a> Rating






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| ID | uint64 (formatted integer)| `uint64` |  | |  |  |
| MethodType | [MethodType](#method-type)| `MethodType` |  | |  |  |
| MethodTypeID | uint64 (formatted integer)| `uint64` |  | |  |  |
| Score | double (formatted number)| `float64` |  | |  |  |
| Severity | string| `string` |  | |  |  |
| Vector | string| `string` |  | |  |  |



### <a id="source"></a> Source






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| DeletedAt | [DeletedAt](#deleted-at)| `DeletedAt` |  | |  |  |
| Host | string| `string` |  | |  | `gitlab.com` |
| ID | uint64 (formatted integer)| `uint64` |  | |  |  |
| Images | [][Image](#image)| `[]*Image` |  | |  |  |
| Organization | string| `string` |  | |  | `vmware` |
| Packages | [][Package](#package)| `[]*Package` |  | |  |  |
| Repository | string| `string` | ✓ | |  | `myproject` |
| Sha | string| `string` | ✓ | |  | `0eb5fcd1` |



### <a id="string-array"></a> StringArray




[]string

### <a id="vulnerability"></a> Vulnerability






**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| CNA | string| `string` |  | |  |  |
| CVEID | string| `string` | ✓ | |  | `CVE-7467-2020` |
| Description | string| `string` |  | |  |  |
| ID | uint64 (formatted integer)| `uint64` |  | |  |  |
| Packages | [][Package](#package)| `[]*Package` |  | |  |  |
| Ratings | [][Rating](#rating)| `[]*Rating` |  | |  |  |
| References | [StringArray](#string-array)| `StringArray` |  | |  |  |
| URL | string| `string` |  | |  |  |

