

# 1. 엘리먼트 렌더링 하기

> ## #root element에 엘리먼트 렌더링

### index.html
![image](https://github.com/Project-Division/about_react/assets/68108664/bcedc75b-a404-43af-94e3-dc23bb129315)

### App.js
```javascript
var App = () => {
  return (
      <div>
        <h1>Hello World!</h1>
      </div>
  )
};

export default App;
```

### index.js
```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

![image](https://github.com/Project-Division/about_react/assets/68108664/b3b3e8c9-8d17-4369-902c-3480b60543bf)


---