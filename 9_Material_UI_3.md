# 5. Skeleton

- ### 로드 시간에 따른 불만을 줄이기 위해 데이터가 로드되기 전에 콘텐츠의 자리에 미리 보기를 표시

<p align="center">

![image](https://github.com/Project-Division/about_react/assets/68108664/e5eceff2-04c3-4146-8050-916cfb1be618) | ![image](https://github.com/Project-Division/about_react/assets/68108664/c6465c81-ae07-4f70-8e9b-5308e3757288)
--- | --- |

</p>

<br>

- ### 사용 예
    - #### item_info가 null이 아닐때 정보를 표시하고, null일 경우 Skeleton을 렌더링
        ```javascript
        {item_info ? (item_info["제조사"]) : (<Skeleton variant="text" sx={{ fontSize: "14px" }} />)}
        ```

<br>

- ### 1. 아이템을 카드 형태로 표시하는 Component 작성

    ![image](https://github.com/Project-Division/about_react/assets/68108664/b0bbd4ce-0019-4217-9efd-8bdd0e8eee8f)

    <br>

    ```javascript
    import Card from '@mui/material/Card';
    import CardContent from '@mui/material/CardContent';
    import Typography from '@mui/material/Typography';
    import Skeleton from '@mui/material/Skeleton';

    const card_style = {
        flexGrow: 1,

        margin: "20px",
        width: "300px"
    };

    const Card_Item = (props) => {
        var item_info = props.item_info;

        return (
            <Card variant="outlined" sx={{ minWidth: 275 }} style={card_style}>
                <CardContent>
                    <Typography sx={{ fontSize: 14 }} color="text.secondary" gutterBottom>
                        {item_info ? (item_info["제조사"]) : (<Skeleton variant="text" sx={{ fontSize: "14px" }} />)}
                    </Typography>
                    <Typography variant="h5" component="div">
                        {item_info ? (item_info["display_name"]) : (<Skeleton variant="text" sx={{ fontSize: "24px" }} />)}
                    </Typography>
                    <Typography sx={{ mb: 1.5 }} color="text.secondary">
                        {item_info ? (item_info["무게"]) : (<Skeleton variant="text" sx={{ fontSize: "16px" }} />)}
                    </Typography>
                    <Typography variant="body2">
                        {item_info ? (item_info["URL"]) : (<Skeleton variant="text" sx={{ fontSize: "14px" }} />)}
                    </Typography>
                </CardContent>
            </Card>
        );
    }
    ```

<br>

- ### 2. 데이터가 로드되지 않았을 때 Skeleton이 렌더링되는지 확인하기 위하여 setTimeout을 이용하여 2초 후에 데이터를 초기화하도록 코드 작성

    ```javascript
    const [data_obj, set_data_obj] = React.useState([]);

    const init_data_obj = () => {
        const data_list = `[{"index":14987,"prod_code":"33362201","제조사":"삼성전자","이름":"갤럭시북4 프로 NT940XGK-KP71S (SSD 512GB)","모델명":"NT940XGK-KP71S","운영체제":"윈도우11홈","인치":"35.6cm(14인치)","해상도":"2880x1800(WQXGA+)","최대밝기":"400nit","주사율":"120Hz","CPU 제조사":"인텔","CPU 세대":"코어 울트라7","CPU 명":"155H (4.8GHz)","CPU 코어 수":"16코어(6P+8E+2LE)","램 규격":"LPDDR5x(온보드)","램 용량":"32GB","램 교체 가능 여부":"불가능","GPU 타입":"내장그래픽","GPU 명":"Arc","GPU TGP":"","GPU VRAM":"","저장장치 인터페이스":"M.2(NVMe)","저장장치 용량":"512GB","저장장치 슬롯 수":"2개","무선랜":"802.11ax(Wi-Fi 6E)","유선랜":"","웹캠":"O","배터리 용량":"63Wh","어댑터":"65W","충전단자":"타입C","두께":"11.6mm","무게":"1.23kg","색상":"실버","HDMI":"HDMI 2.1","D-SUB":"","Mini DP":"","썬더볼트3":"","썬더볼트4":"2개(USB-C겸용)","USB-A":"1개","메모리카드":"O","지문인식":"O","전용 펜":"","PD충전":"O","URL":"https://prod.danawa.com/info/?pcode=33362201&amp;cate=112758","display_name":"갤럭시북4 프로 NT940XGK-KP71S"}, ... }]`;
        set_data_obj(JSON.parse(data_list));
    };

    React.useEffect(() => {
        setTimeout(init_data_obj, 2000); // 2초 후 데이터 초기화 함수 실행
    }, []);
    ```

<br>

- ### 3. 데이터가 로드되지 않았을 때 props.item_info가 null인 Card_Item을 렌더링하고, 로드되었을 때 아이템 정보가 있는 Card_Item을 렌더링하는 컴포넌트 작성

    ```javascript
    const contents_style = {
        display: "flex",
        flexDirection: "row",
        flexWrap: "wrap"
    };

    const Card_Items = () => {
        if (data_obj.length > 0) { // 데이터가 로드되었을 때
            return (
                <div className={"contents"} style={contents_style}>
                    {data_obj.map((item) => (
                        <Card_Item item_info={item} key={item["prod_code"]}/> <!--- item_info 파라미터로 현재 아이템 정보 사용 --->
                    ))}
                </div>
            );
        } else { // 로드되지 않았을 때
            let null_list = [];
            for (let i = 0; i < 12; i++) {
                null_list.push(i);
            } // null_list = [0, 1, 2, ..., 11]

            return (
                <div className={"contents"} style={contents_style}>
                    {null_list.map((item) => (
                        <Card_Item item_info={null} key={`empty_item_${item}`}/> <!--- item_info가 null인 Card_Item 렌더링 --->
                    ))}
                </div>
            );
        }
    }
    ```

<br>

- ### 4. 메인 컴포넌트 작성

    ```javascript
    import React from 'react';

    ...

    const Material_UI_2 = () => {
        ...

        return (
            <div>
                <h1>Notebook Items</h1>
                <Card_Items />
            </div>
        );
    }

    export default Material_UI_2;
    ```

<br>

### 이미지를 클릭해주세요!
![Honeycam 2024-03-24 12-55-24](https://github.com/Project-Division/about_react/assets/68108664/dd202979-68ea-4f5d-be64-886949c75a15)

---
<br><br>

