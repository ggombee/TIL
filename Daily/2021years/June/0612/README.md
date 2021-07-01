# 2. TypeScript (TSC)

1. **~~Transpiling~~** → Babel로 대체 (babel-plugin-typescript)
    - TypeScript → JavaScript
    - 대체 시 Type Checking 기능 없음

2. **Type Checking**
    - 타입이 맞는지 아닌지 체크?

        ex) tsc —moEmit

    - Language Server
        - `tsc`를 돌리지 않아도 VS Code에서 빨간줄을 볼수있는 이유

3. 결론 
    - 레버리징 : 지렛대를 이용함?
    - TypeScript로 타입 체킹 + Babel로 Transpile —> 지속적 개선을 위해
