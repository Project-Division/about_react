# useEffect

- ## use_state 함수
    ```javascript
        const [count, setCount] = useState(0); 
    ```

    - ### 상태의 기본값을 useState의 파라미터로 넣어서 호출
    - ### [현재 상태 변수, Setter 함수] 형태의 배열 반환

<br>

- ## use_effect 함수
    - ### 컴포넌트가 렌더링 이후에 어떤 일을 수행할지 알려주는 역할을 함

    - ### useEffect(수행할 함수, 배열)
        - ### 비어있는 배열 사용
            - #### 최초 렌더링시에만 수행
        - ### 변수가 있는 배열 사용
            - #### 최초 렌더링, 특정 변수가 변경되었을 때 수행

---
<br><br>

# Usage
- ## use_effect_1.js
    ```javascript
    import React from 'react';

    const Use_Effect_1 = () => {
        const [count, setCount] = React.useState(0);
        const countUp = () => { setCount(count + 1) };

        React.useEffect(() => {
            console.log(`count changed to ${count}!`);
        });

        return (
            <div>
                <p>Count: {count}</p>
                <button onClick={countUp}>Count Up</button>
            </div>
        );
    };

    export default Use_Effect_1;
    ```

<br>

- ## index.js
    ```javascript
        import Use_Effect_1 from './use_effect_1'

        ...

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(
            <BrowserRouter>
                <Routes>
                    <Route path="/use_effect_1" element={<Use_Effect_1 />}></Route>
                </Routes>
            </BrowserRouter>
        );

        ...
    ```

<br>

### use_effect_1 렌더링이 완료되었을 때, count가 변경될 때 마다 콘솔에 로그가 출력되고 카운트가 1만큼 증가함.

<br>

![image](https://github.com/Project-Division/about_react/assets/68108664/5ea1b817-4759-4c2f-a8b7-ed87fcff2e4c)