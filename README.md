# Netlas.io Python SDK

This is a Netlas.io Python package with CLI tool.

Please, refer to the documentation to learn where to get an API key and what technical limits exist.

[Documentation &rarr;](https://docs.netlas.io/automation/)

<span class="hide-on-import">[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)</span>

## Installation

Installation:

```
$ pip install netlas
```

Or if you already have it installed and want to upgrade to the latest version:

```
$ pip install --upgrade netlas
```

## API usage

The following code sample routes the request `port:7001` to the Netlas response search and prints search results to stdout.

```
import netlas

apikey = "YOUR_API_KEY"

# create new connection to Netlas
netlas_connection = netlas.Netlas(api_key=apikey)

# retrieve data from responses by query `port:7001`
netlas_query = netlas_connection.query(query="port:7001")

# iterate over data and print: IP address, port, path and protocol
for response in netlas_query['items']:
    print(f"{response['data']['ip']}:{response['data']['port']}{response['data']['path']} [{response['data']['protocol']}]")
pass
```

## CLI usage

Show global help:
```
user@pc:~$ netlas --help
Usage: netlas [OPTIONS] COMMAND [ARGS]...

Options:
-h, --help  Show this message and exit.

Commands:
    count     Calculate count of query results.
    download  Download data.
    host      Host (ip or domain) information.
    indices   Get available data indices.
    profile   Get user profile data.
    query     Search query.
    savekey   Save API key to the local system.
    stat      Get statistics for query.
```

Show specific command help:
```
user@pc:~$ netlas query --help
Usage: python -m netlas query [OPTIONS] QUERYSTRING

Search query.

Options:
-d, --datatype [response|cert|domain|whois-ip|whois-domain]
                                Query data type  [default: response]
-a, --apikey TEXT               User API key (can be saved to system using
                                command `netlas savekey`)
-f, --format [json|yaml]        Output format  [default: yaml]
--server TEXT                   Netlas API server  [default:
                                https://app.netlas.io]
--indices TEXT                  Specify comma-separated data index
                                collections
-i, --include TEXT              Specify comma-separated fields that will be
                                in the output NOTE: This argument is
                                mutually exclusive with  arguments: [-e,
                                exclude].
-e, --exclude TEXT              Specify comma-separated fields that will be
                                excluded from the output NOTE: This argument
                                is mutually exclusive with  arguments:
                                [include, -i].
-p, --page INTEGER              Specify data page  [default: 0]
-h, --help                      Show this message and exit.
```

## Bootstraping

You may want to registry your API key.

```
netlas query savekey YOUR_API_KEY
```
netlas as now saved your key, you can now use the CLI as such:
```
netlas query 'THE_QUERY'
```
