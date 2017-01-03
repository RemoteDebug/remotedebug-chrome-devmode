remotedebug-chrome-devmode
——————————————————————————————————————————————

Chrome extension that allows a developer mode which allows editors to connect to Chrome.

# Usage
100% transparent for 3rd party tools.
Core debugger attaches to local WS server.
Works as if Chrome were started with remote debugging enabled.

# Architecture
Chrome extension with debugger permissions required to get access to the debugger API without starting chrome with specific flag. 

# Chrome extension 
-> Polling every 1000ms for http://localhost:9333
-> Connection ->
-> Start WS server
-> on Browser.getTargets command -> Debugger.getTargets
-> on Browser.attach command -> Debugger.attach
-> Debugger.onMessage -> send back over WS and reverse.

# Node server:
Exposes WS and HTTP endpoint.







