# fastapi-ai-reference
cogvlm

vllm

stable diffusion

invoke ai

https://github.com/invoke-ai/InvokeAI/tree/main/invokeai%2Fapp%2Fapi


https://github.com/Kludex/fastapi-tips?tab=readme-ov-file#2-be-careful-with-non-async-functions
tips
1.
uvicorn에는 기존의 비동기 event loop 나 http parser보다 빠른 uvloop이나 httptools가 없어서
![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/39d63682-dcf8-4ffd-aada-f6826be18d3a)

env에 추가하면 uvicorn이 자동적으로 이를 사용

2. 비동기가 아닌 함수에 주의

![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/229df540-ee58-4b45-9dd4-62d7adce4e95)

3.Websocket에서는 While True보다 async for을 사용

![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/bd7481ff-0f77-45c0-bd0b-383287958f0e)

4. WebSocketDisconnect exception 무시

![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/852b5a45-ef0d-4463-b0cb-a8e3d7e4a71e)

5.TestClient말고  HTTPX의 AsyncClient를 사용

![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/a8179d21-92a5-4ff7-9a62-bcc800746128)

6.app.state 대신에 lifespan state 사용
FastAPI는 lifespan 이벤트를 제공하며, 여기에 on_startup, on_shutdown 등의 이벤트 핸들러를 등록 가능. 이 handler 내에서 상태를 초기화하고 공유하면 다중 워커 환경에서도 상태가 올바르게 관리가능

![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/789792e0-d3ef-4171-a68a-b15cccbf9c1e)
![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/e412ed6a-ef09-4654-aa24-fb9ba345ef3c)

7. BaseHTTPMiddleware 보다 순수한 ASGI Middleware 사용

8. 
