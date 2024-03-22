# Array.map Method

- #### 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환하는 함수

- #### Example
    ```javascript
    let arr = [1, 2, 3, 4, 5]
    let new_arr = arr.map((item) => {
        return item * 2
    });
    console.log(new_arr);
    ```

    ```
    [ 2, 4, 6, 8, 10 ]
    ```

- #### 배열에 들어있는 데이터를 렌더링하기 위해 일반 데이터 배열을 리액트 엘리먼트 배열로 바꾸기 위하여 사용

---
<br><br>

# 예제

- ### 1. 데이터 객체 초기화

    ```javascript
    const [data_obj, set_data_obj] = React.useState([]);

    const init_data_obj = () => {
        const data_list = `[{"index":14987,"prod_code":"33362201","제조사":"삼성전자","이름":"갤럭시북4 프로 NT940XGK-KP71S (SSD 512GB)","모델명":"NT940XGK-KP71S","운영체제":"윈도우11홈","인치":"35.6cm(14인치)","해상도":"2880x1800(WQXGA+)","최대밝기":"400nit","주사율":"120Hz","CPU 제조사":"인텔","CPU 세대":"코어 울트라7","CPU 명":"155H (4.8GHz)","CPU 코어 수":"16코어(6P+8E+2LE)", ... }]`;
        set_data_obj(JSON.parse(data_list));
    };

    React.useEffect(() => {
        init_data_obj();
    }, []); // 무한 루프 방지를 위해 useEffect에서 데이터 객체 초기화
    ```

    ![image](https://github.com/Project-Division/about_react/assets/68108664/7ca3cc56-34ec-4807-8f72-7b6c289cee42)

    - ### Too many re-renders. React limits the number of renders to prevent an infinite loop.

        - #### React는 state에 변화가 발생하면 다시 렌더링을 수행하게 되는데, 이 때 state를 변경시키는 setter 함수가 실행되게 되면 무한 루프에 빠지게 된다.

        - #### 이를 해결하기 위하여 처음 렌더링 되었을때만 실행하는 __React.useEffect(메소드, [])__ 를 이용하였다.

<br>

- ### 2. 렌더링을 위한 간단한 코드 작성

    ```javascript
    const div_style = {
        display: "flex",
        flexDirection: "column",
        alignItems: "center",

    };

    const contents_style = {
        display: "flex",
        flexDirection: "row",
        flexWrap: "wrap"
    }

    const card_style = {
        display: "flex",
        flexDirection: "column",

        border: "1px solid black",

        padding: "15px",
        margin: "15px",
        width: "300px"
    };

    return (
        <div className={"map_1"} style={div_style}>
            <h1>Item List</h1>

            <div className={"contents"} style={contents_style}>
                {data_obj.map((item) => (
                    <div className={"card"} style={card_style}>
                        <p className={"prod_code"}>제품 코드: {item.prod_code}</p>
                        <p className={"manu"}>제조사: {item.제조사}</p>
                        <p className={"name"}>{item.display_name}</p>
                    </div>
                ))}
            </div>
        </div>
    );
    ```

    <br><br>

    - ### Map을 사용하였을 때 변경된 HTML코드
        ```javascript
        {data_obj.map((item) => (
            <div className={"card"} style={card_style}>
                <p className={"prod_code"}>제품 코드: {item.prod_code}</p>
                <p className={"manu"}>제조사: {item.제조사}</p>
                <p className={"name"}>{item.display_name}</p>
            </div>
        ))}
        ```

        <br>

        ![image](https://github.com/Project-Division/about_react/assets/68108664/a4d07595-d805-47e5-a49e-092847afa130)
