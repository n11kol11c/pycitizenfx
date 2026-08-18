# pycitizenfx

Python type annotations for the [CitizenFX](https://www.citizenfx.com/) (FiveM / RedM / LibertyM) scripting API.

Provides full IDE autocompletion, type checking, and documentation for writing FiveM resources in Python.

## Installation

Copy the `annotations/` directory into your project:

```
your_project/
├── annotations/
│   ├── client/
│   └── server/
└── main.py
```

Or add this repo as a git submodule / dependency.

## Usage

```python
import annotations as citizenfx
from annotations.client import on, emitNet, setTick, AddBlipForCoord
from annotations.server import CreateVehicle, GetPlayerName
```

### Client Example

```python
from annotations.client import on, emitNet, setTick, console

@on("myCustomEvent")
def handle_event(args):
    console.log("Event received:", args)

setTick(lambda: console.log("running every frame"))

emitNet("serverEvent", "hello")
```

### Server Example

```python
from annotations.server import on, GetPlayerName, console

@on("playerJoined")
def on_player_join(source):
    name = GetPlayerName(source)
    console.log(f"Player joined: {name}")
```

## Project Structure

```
annotations/
├── __init__.py                 # Re-exports client and server modules
├── client/
│   ├── __init__.py             # Client API exports
│   ├── client_index.py         # Core client types, classes, and framework API
│   ├── natives_universal.py    # All GTA V client native functions (~65k lines)
│   └── *.pyi                   # Type stubs for each module
└── server/
    ├── __init__.py             # Server API exports
    ├── server_index.py         # Core server types, classes, and framework API
    ├── natives_server.py       # Server-side native functions
    └── *.pyi                   # Type stubs for each module
```

## What's Included

- **Client API** — Events, timers, NUI, exports, console, state bags, entity/player helpers
- **Server API** — Events, player management, entity creation, KVP storage, convars, resource management
- **Native Functions** — Full GTA V native function database (client + server) with parameter types, return types, and docstrings
- **Type Stubs** — `.pyi` files for every module

## Requirements

- Python 3.10+ (uses `int | float` union syntax)

## Notes

These are type annotations only — all function bodies are stubs (`pass`). The actual runtime implementation is provided by the FiveM/CitizenFX runtime. This package exists to enable IDE support (autocompletion, type checking, hover docs) when writing Python-based FiveM resources.
