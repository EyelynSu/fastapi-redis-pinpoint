# FastAPI + aioredis Example
Fork from: https://github.com/redis-developer/fastapi-redis-tutorial

### Add Pinpoint
1. Install pinpointPy
```
pip install pinpointPy
```
2. Add below settings in app/main.py
```
# pinpoint
##############################################
from starlette_context.middleware import ContextMiddleware
from starlette_context import context, plugins

from pinpointPy import set_agent
from pinpointPy.Fastapi import asyn_monkey_patch_for_pinpoint
from starlette.middleware import Middleware
from pinpointPy.Fastapi import PinPointMiddleWare

middleware = [
    Middleware(ContextMiddleware),
    Middleware(PinPointMiddleWare)
]
asyn_monkey_patch_for_pinpoint()
set_agent("fastapi-redis", "fastapi-redis", 'tcp:collect-agent:9999', -1, True)
##############################################

```
3. Start server and request
```
uvicorn main:app --host=0.0.0.0
curl -X POST host:port/refresh
curl host:port/is-bitcoin-lit
```
