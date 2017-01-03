# remotedebug-chrome-devmode
------

Chrome extension that allows a developer mode which allows editors to connect to Chrome.

## Usage
100% transparent for 3rd party tools.
Core debugger attaches to local WS server.
Works as if Chrome were started with remote debugging enabled.

## Architecture
```
                                      │

                                      │
    ┌───────────────────────────┐           ┌───────────────────────────┐
    │                           │     │     │                           │
    │          Chrome           │           │          VS Code          │
    │                           │     │     │                           │
    └───────────────────────────┘           └───────────────────────────┘
    ┌───────────────────────────┐     │
    │  DevMode Chrome exension  │
    └───────────────────────────┘     │
                  ▲
                  │                   │
  socket.io / ws  │                         ┌───────────────────────────┐
                  │                   │     │      Chrome debugger      │
                  ▼                         └───────────────────────────┘
    ┌───────────────────────────┐     │     ┌───────────────────────────┐
    │    DevMode node server    │◀─────────▶│   Chrome core debugger    │
    └───────────────────────────┘     │     └───────────────────────────┘
             WS server
                                      │

                                      │

                                      │

```
A Chrome extension with debugger permissions required to get access to the debugger API without starting chrome with specific flag. The chrome extension can then connect to a local node server over WS/socket.io and forward the messages over a real WS server, which any regular CDP client can connect to. This way it's fully transparent to clients.

### Chrome extension 
-> Polling every 1000ms for ex http://localhost:9333
-> Connection ->
-> Start WS server
-> on Browser.getTargets command -> Debugger.getTargets
-> on Browser.attach command -> Debugger.attach
-> Debugger.onMessage -> send back over WS and reverse.

### Node server:
Exposes WS and HTTP endpoint.







