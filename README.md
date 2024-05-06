# fastapi-ai-reference
cogvlm
vllm
tips
1.
uvicorn에는 기존의 비동기 event loop 나 http parser보다 빠른 uvloop이나 httptools가 없어서
![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/39d63682-dcf8-4ffd-aada-f6826be18d3a)
env에 추가하면 uvicorn이 자동적으로 이를 사용
2. 비동기가 아닌 함수에 주의
![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/229df540-ee58-4b45-9dd4-62d7adce4e95)
3.Websocket에서는 While True보다 async for을 사용
![image](https://github.com/jinuk0211/fastapi-ai-reference/assets/150532431/bd7481ff-0f77-45c0-bd0b-383287958f0e)

