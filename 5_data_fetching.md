# React에서 서버로 부터 데이터를 가져오는 방법

- ### React에서는 서버 사이드 렌더링을 이용하기 어려움
    ### => Axios를 이용하여 서버의 API에서 정보를 가져와 동적으로 렌더링

---
<br><br>

# 1. 세팅
- ## Axios 라이브러리 설치
    ```
    npm install axios
    ```
<br>

- ## CORS 해결
    - ### CORS란?
        ```
        Cross Origin Resource Sharing의 약자로,
        현재 웹페이지 도메인에서 다른 웹페이지 도메인으로 리소스가 요청되는 경우
        브라우저 자체에서 보안 상 이유로 CORS를 제한하게 되는 현상을 말합니다.
        ```
    
    

    - ### Client에서의 해결 방법
        - #### http-proxy-middleware 설치
            ```
            npm install http-proxy-middleware --save
            ```

        - #### src 디렉토리에 setupProxy.js 생성
            ```javascript
            const { createProxyMiddleware } = require('http-proxy-middleware');

            const api_server_addr = 'http://localhost:3001';

            module.exports = function(app) {
                app.use(
                    createProxyMiddleware("/api",{
                        target: api_server_addr,
                        changeOrigin: true,
                    })
                )
            };
            ```


---
<br><br>

# 2. 현재 시간을 문자열 형태로 리턴하는 API 작성

- ### api.js
    ```javascript
    const router = require("express").Router();

    const api_router = router.get("/current_datetime/", (req, res, next) => {
        res.send(new Date().toLocaleString());
    });

    module.exports = {
        api_router
    };
    ```

- ### index.js
    ```javascript
        ...

        const {api_router} = require("./routes/api");
        app.use("/api", api_router);

        ...
    ```

<br>

![image](https://github.com/Project-Division/about_react/assets/68108664/f23f9691-f86a-4372-9ae6-49cf264cd821)

---
<br><br>

# 3. 클라이언트 코드 작성

- ### data_fetching_1.js
    ```javascript
    import React from 'react';
    import Axios from 'axios';

    const get_datetime_from_server = async () => {
        try {
            let response_data = await Axios.get(`/api/current_datetime`);
            return response_data.data;
        } catch (err) {
            console.log(err);
        }
        return "";
    };

    const Data_Fetching_1 = () => {
        const [curr_datetime, setCurrDatetime] = React.useState("");

        React.useEffect(() => {
            const fetch_data = async () => {
                setCurrDatetime(await get_datetime_from_server());
            }
            fetch_data();
            console.log(curr_datetime);
            setInterval(fetch_data, 500); // 500ms 간격으로 fetch_data 계속 실행
        }, []); // 요소가 처음 렌더링 되었을때만 실행

        return (
            <div>
                <p>{curr_datetime}</p>
            </div>
        );
    };

    export default Data_Fetching_1;
    ```

<br>

- ### index.js
    ```javascript
    ...

    import Data_Fetching_1 from './data_fetching_1';

    ...

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
        <BrowserRouter>
            <Routes>
                <Route path="/data_fetching_1" element={<Data_Fetching_1 />}></Route>
            </Routes>
        </BrowserRouter>
    );

    ...
    ```

<br>

![image](https://github.com/Project-Division/about_react/assets/68108664/0b505374-5405-46f3-9e71-9e74df2ed265)