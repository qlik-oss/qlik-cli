# Changelog

## 2.10.1

- Improvement: More network logs! Now the `--verbose` flag will properly display network information related to the establishing of websockets. Previously, this only applied to pure HTTP-requests.

- Fix: Websocket specific flags will now be properly displayed for websocket-based commands. Note: as part of this work some flags that were previously present, but hidden, on the root command are now only present where they are useful. Scripts using a blanket-set of undocumented flags may need updating.

- Fix: Updated descriptions for edit commands. The descriptions will state clearly which editor will be opened upon command execution and how the editor is chosen.

- Improvement: Support for query-parameters of type array.

- Fix: More robust handling of server-types.

- Fix: Minor improvements to multipart request handling.

- Fix: Added `--quiet` flag to `bookmark ls` command.

## 2.9.0

- Improvement: The verbose logging for HTTP requests, accessible through the flag `--verbose` or `-v`, is now enhanced to include information about the connections being made. The new logs concering connections are prefixed with an asterisk.

## 2.8.0

- New: `qlik spec get <api-spec>` has been improved to show more information about added specifications. It will now show a complete, detailed list of commands added from the specification. This can give insight into how the API specifications are interpreted.

- New: For commands that send arrays of JSON-objects the description on how to do so will be more descriptive and verbose - explaining what fields the objects contain. The flag descriptions also
wrap to about 80 characters in width (in most cases). Check out `qlik license assignment add` for an example.

- Fix: Resolved an issue that caused the `qlik app ls` command to not be displayed correctly in help and auto-completion.

- Fix: The `qlik update` command on Windows has been fixed. There was an issue with updating the running binary that is now handled.

- Fix: Some arguments contain leading hyphens which cause the arguments to be interpreted as flags. In most of these cases, a text explaining how this can be prevented with the use of double-dashes will appear. (For example: `qlik app get -- -my-app`)

## 2.7.0

- New: Added flags to `qlik app ls`. Some of the things that can be controlled with the flags are
include only apps for a specific user or exclude apps for a specific user and control sort order.

    example:
    ```bash
    # created by user, latest first
    qlik app ls --createdByUserId <user-id> --sort -createdAt
    # not created by user, oldest first
    qlik app ls --notCreatedByUserId <user-id> --sort +createdAt
    ```

- Fix: Improved handling of allOf-schemas and get latest reload spec.

## 2.6.0

- New: Added `qlik edit` command - you can now easily update resources without worrying about 
the complicated JSON Patch calculations, based on the `EDITOR` environment variable, the edit 
command will start automatically your preferred editor and once you changes are saved, will 
do all the PUT/PATCH work for you.

    *If you want to see communication details for your edit call you can use the `--verbose` 
    flag. This will display all HTTP operations that are performed including payloads for requests.*

    example:
    ```bash
    qlik webhook edit <webhookId>
    # this command will launch your preferred editor containing the resource in json format
    # changing for example the description parameter and save will be the equivalent of doing 
    # a patch with payload:
    # [
    #   {
    #       "op": "replace",
    #       "path": "/description",
    #       "value": "my new description"
    #   }
    # ]
    ```

- New: Added `qlik spec get` provides more detailed information about added external specs, most notably the path to the added specification.

- New: The auto-generated usage documentation now get automatically published to https://qlik.dev/libraries-and-tools/qlik-cli upon new releases.

- Fix: Improved robustness in handling of array subtypes - missing types will now return errors. Any included schema is thus required to have proper types defined. Previously, we defaulted to string if the type was missing.


## 2.5.1

- Fix: YAML-spec support

## 2.5.0

- New: Added support for outbound proxy: you can now set the operating system environment variables called `HTTPS_PROXY/HTTP_PROXY` with the hostname or IP address of the proxy server. _Note:_ `HTTPS_PROXY` takes precedence over `HTTP_PROXY` for https requests. Qlik CLI supports only Basic Authentication.

- Fix: Improve --limit flag descriptions

- Fix: Updated the included QCS API-specifications

## 2.4.2
- Fix: CI pipeline release

## 2.4.1
- Fix: CI pipeline release

## 2.4.0

- New: Commands have been updated to reflect the latest API changes.

- New: Notify users when a new version of qlik-cli is available. The notification message contains URL with detailed changelog of the latest release.

- New: Added self update command that enables users to update to the latest version of qlik-cli by simply running: `qlik update`. One exception here are binaries installed with Chocolatey that will not be updated due to permission restrictions that Chocolatey has on it's binary directory.

- New: Added support for OpenAPI specs that define parameters at the path level. In this case, the parameters are inherited by all operations under that path.

- New: The animated progress bar is now based on estimated upload time.

- New: Better support for unix-like Windows terminals (MingGW, MSYS2, and Cygwin).

- Fix: Various small improvements and bugfixes.


## 2.3.1

- Fix: CI pipeline release
## 2.3.0

- New: adding support for the `identity-providers` endpoint

- New: adding support for the `questions` endpoint

- New: The animated progress bar now also shows on download.

- New: there's a new spinner feedback when waiting for server response.

## 2.2.2

- Fix: Various small improvements and bugfixes.
## 2.2.1

- Fix: Piped input is not supported for Mingw64. Piped input is therefore not supported for the Git BASH for Windows terminal since it uses Mingw64, skip stdin input for Mingw64.

- Fix: Various small improvements and bugfixes.


## 2.2.0

- New: You can now upload large apps to SaaS tenants using qlik-cli using the `qlik app import` command. Use the `--resumable` switch to instruct the cli to handle the upload in chunks which can be resumed if needed. 
When you upload an app using qlik-cli, a nice animated bar appears displaying
the progress.

- New: standard-in piping allows you to combine commands where the output of one may be used
as the input of the next command you issue.

- New: Aliases enable you to create shorthand commands for hard to remember long commands. For example, say you run a command frequently to find the guid of an application in your tenant, `qlik item ls --resourceType app --name`. You can use the alias command to create a shortcut it into something like `qlik getAppGuid consumer+sales`. This returns the complete JSON object for the consumer+sales resource in the items collection.

    Another example:
    ```bash
    qlik alias add my-apps item ls --ownerId=$(qlik user me -q) --resourceType=app
    # Simply calling qlik my-apps will then give you the desired list.
    ```


- New: The `--limit` switch enables you to return a number of app resource objects per page ranging from 1 to 100.

- New: Command switches and flags that are experimental features are labeled as such for your information.

- Fix: Use of the temporary upload service in qlik-cli caused problems with large app uploads and resumability. This problem has been fixed and implemented through the resumable switch in the `qlik app import` command.

- Fix: In prior CLI versions, `qlik reload get` was not sending a correct response. This issue has been resolved.


## 2.1.0

- New: - adding support for the `webhooks` endpoint
- Fix: return status code and description for empty response by default.

## 2.0.0

- New: the `license` command in qlik-cli enables you to set license assignments for
users in addition to providing metrics related to your tenant's overall license
footprint.

- New: the `evaluation` command enables you to trigger Qlik Sense app evaluations
through cli, retrieve the results, and perform additional commands based on the
feedback. A handy command for automating devops of Qlik Sense apps.

- New: Flags that are deprecated in qlik-cli now show a warning message when used.

    ```bash
    qlik api-key ls --sub="test"
    "Flag --sub has been deprecated, please don't use it!"
    ```
- New: You can now add names to external specifications you add into qlik-cli.
Here's an example: `qlik spec add ./my-spec.json --name foo`

- Breaking: The response on the `app` command has changed. Now it returns only information
from the Apps API.

    ```bash
    #qlik app create command
    app=$(qlik app create --attributes-name "example")
    echo $app
    #returns new response

    {
    "attributes": {
        "_resourcetype": "app",
        "createdDate": "2021-02-15T07:01:43.930Z",
        "custom": {},
        "description": "",
        "dynamicColor": "",
        "encrypted": true,
        "hasSectionAccess": false,
        "id": "8be82d0f-02d2-4f0e-974c-08dc444384a7",
        "lastReloadTime": "",
        "modifiedDate": "2021-02-15T07:01:46.575Z",
        "name": "testttt2",
        "originAppId": "",
        "owner": "auth0|b96eb87010c7ad52667b2dc8b1ec0b12f97c43ae7848740874267b62aa45c856",
        "ownerId": "ffnbiWZyssMZ5ofRfLc1JzFdZrPvACFl",
        "publishTime": "",
        "published": false,
        "thumbnail": ""
    },
    "create": [...],
    "privileges": [...]
    }
    ```

    Instead of returning information from the items API.

    ```bash
    #Breaking change

    app=$(qlik app create --attributes-name "example")
    echo $app
    #returns old response

    {
    "actions": [...],
    "collectionIds": [],
    "createdAt": "2021-02-15T08:15:57Z",
    "creatorId": "ffnbiWZyssMZ5ofRfLc1JzFdZrPvACFl",
    "id": "602a2dbd31d6bf3d1f471c31",
    "isFavorited": false,
    "meta": {...},
    "name": "testttt3",
    "ownerId": "ffnbiWZyssMZ5ofRfLc1JzFdZrPvACFl",
    "resourceAttributes": {...},
    "resourceCreatedAt": "2021-02-15T08:15:57Z",
    "resourceCustomAttributes": null,
    "resourceId": "22205ac6-406c-4484-b715-1da12219b044",
    "resourceReloadEndTime": "",
    "resourceReloadStatus": "",
    "resourceSize": {... },
    "resourceSubType": "",
    "resourceType": "app",
    "resourceUpdatedAt": "2021-02-15T08:15:57Z",
    "tenantId": "xrpC13FnjenBc-mhBG98ah2qNlfmwj8X",
    "thumbnailId": "",
    "updatedAt": "2021-02-15T08:15:57Z",
    "updaterId": "ffnbiWZyssMZ5ofRfLc1JzFdZrPvACFl"
    }
    ```

    From now on, to obtain the unique id referencing the app in the items API, you
    need to issue a `qlik item ls` command after running `qlik app create`.

    ```bash
    qlik item ls --resourceId $app --resourceType app
    #returns item information formerly seen in the old response
    ```
- Fix: a security enhancement has been made to remove session Ids from log messages
- Fix: fixed a bug with `qlik app ls` returning non-app resources.
- Fix: fixed `qlik qrs task start by-id` which failed with `no such operation`
  message.
- Fix:  Resolved runtime errors using qlik-cli on Windows computers.

## 1.7.0/1.7.1

- New: adding partial reload capability to qlik app reload
    ```bash
    qlik app reload --app <myapp> --partial
    ```
- New: support for renaming a context
    ```bash
    qlik context rename [flags]
    ```

## 1.6.0

- New: adding support for the `retry-after` headers
- Fix: autocompletion for the `--context` flag
- Fix: automatically renaming parameter names that collide with one of the built-in parameters

## 1.5.1

- Fix: handling of raw-paths

## 1.5.0

- New: experimental support for the QRS API in Qlik Sense for Windows.
- New: - `--server-type` flag: the type of server you are using: cloud (SaaS), windows (Enterprise on Windows) or engine
- Fix: adds sorting to the body parameters for multipart, earlier `data` and `file` could be returned in random order.
- Fix: minor bug-fixes and release pruning

## 1.4.0

- Breaking: new standard renaming arguments and flags called only `id`, these will now be exposed as <resource>Id instead.
    ```bash
    qlik extension file get <filepath> -id <extensionId>
    # should now be
    qlik extension file get <filepath> -extensionId <extensionId>
    ```
- Fix: adding limits `(default, max and min)` to the parameter description if present in the specification.
- Fix: operations with unsupported content-types are now detected and, when used, will throw an error message ex: `unsupported content-type <content-type>`
- Fix: updating latest specs

## 1.3.0/1.3.1

- New: commands for publishing/unpublishing generic objects ex: make sheet public
    ```bash
    qlik app object publish <object-id> [flags]
    qlik app object unpublish OBJECT-ID -a APP-ID
    ```
- New: `--retry` and `--interval` flags which are used to set the number of retries and with what interval they should be done.
- Fix: detect parameter collisions in order to avoid inevitable panic.

## 1.2.0

- New: support for the `quotas` and `users` endpoints

## 1.1.0

- New: support for the `extension` and `theme` endpoints

## 1.0.0

Initial public release.
