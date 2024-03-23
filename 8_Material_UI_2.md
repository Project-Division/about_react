# 1. 버튼 배치

- ### 버튼 배치를 위한 코드 작성

    ```javascript
    import React from "react";

    ...

    const material_ui_1_style = {
        display: "flex",
        flexDirection: "column"
    };

    const button_ex_1_style = {
        display: "flex",
        flexDirection: "row",
        alignItems: "center",
        justifyContent: "center",

        margin: "20px"
    };

    const button_style = {
        flexGrow: 1,
        maxWidth: "200px",
        marginRight: "20px",
    }

    ...

    const Material_UI_1 = () => {
        return (
            <div>
                <div className={"material_ui_1"} style={material_ui_1_style}>
                    <Alert_Success/>

                    <div className={"button_ex_1"} style={button_ex_1_style}>
                        <Button variant="outlined" style={button_style} onClick={button_1_event}>BUTTON 1</Button>
                        <Button_2/>
                        <Button_3/>
                    </div>
                </div>

                <Snackbar_1 />
            </div>

        )
    }

    export default Material_UI_1;
    ```

![image](https://github.com/Project-Division/about_react/assets/68108664/1deaf296-0cd1-458e-a1bb-ded4b1f54666)

---
<br><br>

# 2. 간단한 버튼과 버튼 이벤트 등록

- ### https://mui.com/material-ui/react-button/

- ### 버튼 추가
    ```javascript
    import Button from '@mui/material/Button';

    ...

    const button_1_event = () => {
        alert("button 1 clicked!");
    }

    <Button variant="outlined" style={button_style} onClick={button_1_event}>BUTTON 1</Button>

    ...
    ```

    <br>

![Honeycam 2024-03-23 12-15-06](https://github.com/Project-Division/about_react/assets/68108664/c6403ed9-2c2d-44c4-95ab-2adf54fc7b74)

---
<br><br>

# 3. Alert

- ### https://mui.com/material-ui/react-alert/

    ![image](https://github.com/Project-Division/about_react/assets/68108664/a82a3f6b-04df-4ffc-b9dd-483796c0b93d)

<br>

- ### Alert 생성

    ```javascript
    var set_alert_displaying = null; // 버튼 이벤트에서 alert 속성값을 변경하기 위한 전역 선언

    const Alert_Success = () => {
        const [is_displaying, set_displaying] = React.useState(false);
        set_alert_displaying = set_displaying;

        const alert_style = {
            margin: "20px"
        };

        return (
            <Fade in={is_displaying} style={alert_style} unmountOnExit={true}>
                <Alert variant="filled" severity="success">
                    1초 후 사라집니다.
                </Alert>
            </Fade>
        );
    }
    ```

- ### Alert 생성을 위한 버튼 추가

    ```javascript
    const Button_2 = () => {
        const [is_enabled, set_enabled] = React.useState(true);

        const btn_event = (obj) => {
            set_enabled(false);

            set_alert_displaying(true);

            setTimeout(() => {
                set_alert_displaying(false); // 1초 후에 Alert 사라지게 하기
                set_enabled(true); // Alert 사라진 후 버튼 다시 활성화
            }, 1000);
        }

        return (
            <Button variant="contained" color="success" style={button_style} disabled={!is_enabled} onClick={btn_event}>ALERT</Button>
        );
    };
    ```

    <br>

![Honeycam 2024-03-23 12-22-48](https://github.com/Project-Division/about_react/assets/68108664/6a4c6f74-59bc-4898-8fbc-a2b9bb39068a)

---
<br><br>

# 4. Snackbar

- ### https://mui.com/material-ui/react-snackbar/

    ![image](https://github.com/Project-Division/about_react/assets/68108664/635ca070-0e98-418e-84b9-4ccc52acfe6c)

<br>

- ### Snackbar 생성

    ```javascript
    var set_snackbar_status = null; // 버튼 이벤트에서 snackbar 속성값을 변경하기 위한 전역 선언

    const Snackbar_1 = () => {
        const [status, set_status] = React.useState({
            is_displaying: false,
            caller_btn_enabler: null // snackbar가 사라진 이후 버튼 활성화를 위해 속성 변경 함수 넘겨받음
        });
        set_snackbar_status = set_status;

        const on_closed = () => { // HideDuration 이후 실행될 함수
            set_status({
            is_displaying: false, // snackbar 숨기기
            caller_btn_enabler: null
            });

            status["caller_btn_enabler"](); // 버튼 활성화
        };

        return (
            <Snackbar
                open={status["is_displaying"]}
                autoHideDuration={3000}
                onClose={on_closed}
                message="3초 후에 사라집니다."
            />
        );
    }
    ```

<br>

- ### Snackbar 생성을 위한 버튼 추가

```javascript
const Button_3 = () => {
    const [is_enabled, set_enabled] = React.useState(true);

    const btn_event = () => {
        set_enabled(false);

        set_snackbar_status({
            is_displaying: true,
            caller_btn_enabler: () => {
                set_enabled(true);
            }
        });
    };

    return (
        <Button variant="outlined" color="error" style={button_style} onClick={btn_event} disabled={!is_enabled}>SNACKBAR</Button>
    );
}
```

<br>

![Honeycam 2024-03-23 12-31-11](https://github.com/Project-Division/about_react/assets/68108664/51e83fa0-d4fa-4d35-95d7-54ddab43849d)