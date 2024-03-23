# 프론트로 React, 백엔드로 Node.js 사용하기

- ### 1. 리액트 프로젝트 디렉토리에서 명령 실행

   ```
   npm run build
   ```

<br>

<p align="center"><img src="https://github.com/Project-Division/about_react/assets/68108664/86d29ca4-b8d8-4ffa-b71c-2ce548866972" width="800px"></p>

<br>

- ### 2. backend index.js 작성
   ```javascript
   ...

   const path = require("path");
   app.set('views', path.join(__dirname, 'views'));
   app.set('view engine', 'ejs');

   const router = express.Router();
   const main_router = router.get("/", (req, res, next) => {
      res.render("index");
   });
   app.use("/", main_router);

   app.use("/static", express.static(path.join(__dirname, "static")));

   ...
   ```

<br>

- ### 3. 빌드된 파일 중 static 디렉토리를 백엔드의 static 디렉토리로 이동

<br>

- ### 4. 빌드된 파일 중 index.html을 백엔드의 views 디렉토리로 이동