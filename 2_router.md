# 1. 라우터란?

### 사용자가 요청한 URL에 따라 해당 URL에 맞는 페이지를 보여주는 것

---
<br><br>

# 2. 세팅

> 설치
```
npm install react-router-dom
```

> import
```javascript
import {BrowserRouter, Routes, Route} from 'react-router-dom';
```

---
<br><br>

# 3. BrowserRouter

### index.js

<br>

> Route 컴포넌트
#### path 속성에 경로, element 속성에 컴포넌트 넣어줌
<br>

> 사전에 정의되지 않은 경로로 접근하는 경우 처리
#### path="*" 인 라우터를 제일 아래에 추가
<br>

> #### 라우터로 사용할 요소 이름은 대문자로 사용하여야 함.


<br>


```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import {BrowserRouter, Routes, Route} from 'react-router-dom';

import App from './App';
import SubPage1 from './SubPage1'

...

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <BrowserRouter>
        <Routes>
            <Route path="/" element={<App />}></Route>
            <Route path="/subpage1" element={<SubPage1 />}></Route>
        </Routes>
    </BrowserRouter>
);

...
```
<br>

### App.js

<br>

> Link 컴포넌트
#### History API를 통해 브라우저 주소의 경로를 바꾸는 기능이 내장되어 있음

<br>

```javascript
import { Link } from 'react-router-dom';

var App = () => {
  return (
      <div>
          <h1>Hello World!</h1>
          <Link to="/subpage1"><p>서브페이지로 이동</p></Link>
      </div>
  )
};

export default App;
```
<br>

![image](https://github.com/Project-Division/about_react/assets/68108664/e8360933-f4e6-4d95-a779-07bfce2b1388)

<br>

### SubPage1.js
```javascript
import React from 'react';

var SubPage1 = () => {
  return (
      <div>
          <p>서브 페이지1 입니다.</p>
      </div>
  );
};
export default SubPage1;
```
<br>

![image](https://github.com/Project-Division/about_react/assets/68108664/21a0d0a8-ff28-4662-bf61-cea23c28a1b0)

---
<br><br>

# 4. URL파라미터와 쿼리 스트링 사용

### index.js

```javascript
...

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <BrowserRouter>
        <Routes>
            <Route path="/subparam1/:param" element={<SubParam1 />}></Route>
        </Routes>
    </BrowserRouter>
);

...
```

<br>

### subparam1.js
```javascript
import React from 'react';
import { useParams } from 'react-router-dom';

var SubParam1 = () => {
    const {param} = useParams();
    return (
        <div>
            <p>Parameter: {param}</p>
        </div>
    );
};

export default SubParam1;
```

<br>

![image](https://github.com/Project-Division/about_react/assets/68108664/d80a203c-3a49-4ad1-af4d-4304f01dd83a)

---
<br><br>