# NeoFS HTTP Protocol Gateway

NeoFS HTTP Protocol Gateway bridges NeoFS internal protocol and HTTP standard.
- you can download one file per request from NeoFS Network
- you can upload one file per request into the NeoFS Network

## Notable make targets

```
dep          Check and ensure dependencies
image        Build clean docker image
dirty-image  Build diry docker image with host-built binaries
fmts         Run all code formatters
lint         Run linters
version      Show current version
```

## Install

```go get -u github.com/nspcc-dev/neofs-http-gate```

## File uploading behaviors

- you can upload on file per request
- if `FileName` not provided by Header attributes, multipart/form filename will be used instead

## Configuration

```
# Flags:

      --pprof                      enable pprof
      --metrics                    enable prometheus
  -h, --help                       show help
  -v, --version                    show version
      --key string                 "generated" to generate key, path to private key file, hex string or wif (default "generated")
      --verbose                    debug gRPC connections
      --request_timeout duration   gRPC request timeout (default 5s)
      --connect_timeout duration   gRPC connect timeout (default 30s)
      --listen_address string      HTTP gate's listen address (default "0.0.0.0:8082")
  -p, --peers stringArray          NeoFS nodes

# Environments:

HTTP_GW_KEY=string                               - Path to private key file, hex string or wif string
HTTP_GW_CONNECT_TIMEOUT=duration                 - Timeout for connection
HTTP_GW_REQUEST_TIMEOUT=duration                 - Timeout for request
HTTP_GW_REBALANCE_TIMER=duration                 - Time between connections checks
HTTP_GW_LISTEN_ADDRESS=host:port                 - Address to listen connections
HTTP_GW_PEERS_<X>_ADDRESS=host:port              - Address of NeoFS Node
HTTP_GW_PEERS_<X>_WEIGHT=float                   - Weight of NeoFS Node
HTTP_GW_PPROF=bool                               - Enable/disable pprof (/debug/pprof)
HTTP_GW_METRICS=bool                             - Enable/disable prometheus metrics endpoint (/metrics)
HTTP_GW_LOGGER_FORMAT=string                     - Logger format
HTTP_GW_LOGGER_LEVEL=string                      - Logger level
HTTP_GW_LOGGER_NO_CALLER=bool                    - Logger don't show caller
HTTP_GW_LOGGER_NO_DISCLAIMER=bool                - Logger don't show application name/version
HTTP_GW_LOGGER_SAMPLING_INITIAL=int              - Logger sampling initial
HTTP_GW_LOGGER_SAMPLING_THEREAFTER=int           - Logger sampling thereafter
HTTP_GW_LOGGER_TRACE_LEVEL=string                - Logger show trace on level
HTTP_GW_KEEPALIVE_TIME=duration                  - After a duration of this time if the client sees no activity
                                                   it pings the server to see if the transport is still alive 
HTTP_GW_KEEPALIVE_TIMEOUT=duration               - After having pinged for keepalive check, the client waits for a duration
                                                   of Timeout and if no activity is seen even after that the connection
                                                   is closed
HTTP_GW_KEEPALIVE_PERMIT_WITHOUT_STREAM=bool     - If true, client sends keepalive pings even with no active RPCs.
                                                   If false, when there are no active RPCs, Time and Timeout will be
                                                   ignored and no keepalive pings will be sent
HTTP_GW_UPLOAD_HEADER_USE_DEFAULT_TIMESTAMP=bool - Enable/disable adding current timestamp attribute when object uploads

HTTP_GW_WEB_READ_BUFFER_SIZE=4096          - per-connection buffer size for requests' reading
HTTP_GW_WEB_READ_TIMEOUT=15s               - an amount of time allowed to read the full request including body
HTTP_GW_WEB_WRITE_BUFFER_SIZE=4096         - per-connection buffer size for responses' writing
HTTP_GW_WEB_WRITE_TIMEOUT=1m0s             - maximum duration before timing out writes of the response
HTTP_GW_WEB_STREAM_REQUEST_BODY=true       - enables request body streaming, and calls the handler sooner when given 
                                             body is larger then the current limit
HTTP_GW_WEB_MAX_REQUEST_BODY_SIZE=4194304  - maximum request body size, server rejects requests with bodies exceeding
                                             this limit

Peers preset:

HTTP_GW_PEERS_<N>_ADDRESS = string
HTTP_GW_PEERS_<N>_WEIGHT = 0..1 (float)
```
