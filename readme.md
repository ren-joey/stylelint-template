# Stylelint CSS 樣式標準化

本範例參考[Robby - 全端的 Front-End Engineer](https://dotblogs.com.tw/explooosion/1) - [CSS - 運用 Stylelint 養成好習慣](https://dotblogs.com.tw/explooosion/2018/09/30/141005)所完成

<h3 style="font-weight: bold;"><a id="t00">示範環境</a></h3>

本範例使用 mac 終端機<br/>
使用 [Visual Studio Code](https://code.visualstudio.com/) 進行開發

<h3 style="font-weight: bold;"><a id="t01">npm 環境建置</a></h3>

使用 default 參數初始化 npm 環境

```bash
npm init -y
```

<h3 style="font-weight: bold;"><a id="t02">安裝 vscode 擴充功能</a></h3>

- [stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint)<br/>
  <img src="https://az787680.vo.msecnd.net/user/incredible/768eeac2-5183-4869-b725-a06acca5d1b1/1538289428_76378.png" width="300">
- [stylefmt](https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-stylefmt)<br/>
  <img src="https://az787680.vo.msecnd.net/user/incredible/768eeac2-5183-4869-b725-a06acca5d1b1/1538289428_79332.png" width="300">
  <br/>

> 注意: 安裝完畢後須將 vscode 重新啟動

<h3 style="font-weight: bold;"><a id="t03">npm 套件安裝</a></h3>

一鍵安裝

```bash
npm install -D stylelint stylelint-config-prettier stylelint-config-sass-guidelines stylelint-config-standard stylelint-order stylelint-scss pre-commit
```

或依序安裝個別項目

```bash
npm install -D stylelint
npm install -D stylelint-config-prettier
npm install -D stylelint-config-sass-guidelines
npm install -D stylelint-config-standard
npm install -D stylelint-order
npm install -D stylelint-scss
npm install -D pre-commit
```

<h3 style="font-weight: bold;"><a id="t04">config 檔案設定</a></h3>

新增 stylelint 檔案

```bash
touch .stylelintrc.json
```

或者直接使用 vscode 新增該檔案

編輯檔案 _**.stylelintrc.json**_

```json
{
  "extends": [
    "stylelint-config-standard",
    "stylelint-config-prettier",
    "stylelint-config-sass-guidelines"
  ],
  "plugins": [
    "stylelint-scss",
    "stylelint-order"
  ],
  "rules": {
    "max-nesting-depth": null,
    "no-empty-source": null,
    "no-descending-specificity": null,
    "order/properties-alphabetical-order": null,
    "order/properties-order": [
      "position",
      "top",
      "right",
      "bottom",
      "left",
      "display",
      "align-items",
      "justify-content",
      "float",
      "clear",
      "overflow",
      "overflow-x",
      "overflow-y",
      "margin",
      "margin-top",
      "margin-right",
      "margin-bogttom",
      "margin-left",
      "padding",
      "padding-top",
      "padding-right",
      "padding-bottom",
      "padding-left",
      "width",
      "min-width",
      "max-width",
      "height",
      "min-height",
      "max-height",
      "font-size",
      "font-family",
      "font-weight",
      "text-align",
      "text-justify",
      "text-indent",
      "text-overflow",
      "text-decoration",
      "white-space",
      "line-height",
      "color",
      "background",
      "background-position",
      "background-repeat",
      "background-size",
      "background-color",
      "background-clip",
      "border",
      "border-style",
      "border-width",
      "border-color",
      "border-top",
      "border-top-style",
      "border-top-width",
      "border-top-color",
      "border-right",
      "border-right-style",
      "border-right-width",
      "border-right-color",
      "border-bottom",
      "border-bottom-style",
      "border-bottom-width",
      "border-bottom-color",
      "border-left",
      "border-left-style",
      "border-left-width",
      "border-left-color",
      "border-radius",
      "opacity",
      "filter",
      "list-style",
      "outline",
      "visibility",
      "z-index",
      "box-shadow",
      "text-shadow",
      "resize",
      "transition",
      "cursor"
    ],
    "property-no-vendor-prefix": null,
    "selector-max-compound-selectors": null,
    "scss/at-import-partial-extension-blacklist": null,
    "value-no-vendor-prefix": null
  }
}
```
"order/properties-order" 設定參數代表 style 撰寫順序規範，可進行個人化微調<br/>
> 詳細的編成風格設定可參考 [stylelint-order GitHub](https://github.com/hudochenkov/stylelint-order/tree/master/rules/order)

**並且良好的樣式風格應該盡量依序為：**<br/>
1. 間距位置容器設定
2. 背景顏色字體設定
3. 邊框圓角陰影設定
4. 動畫變形設定

<h3 style="font-weight: bold;"><a id="t05">新增 npm 指令</a></h3>

編輯檔案 _**package.json**_
```json
  {
  "scripts": {
      "lint": "stylelint app/scss/**/*.scss --syntax scss",
      "lint:fix": "stylelint app/scss/**/*.scss --syntax scss --fix"
    },
    "pre-commit": [
      "lint"
    ],
  }
```
功能解析：
* "**lint**": 進行 css 程式碼檢查
* "**lint:fix**": 自修動復所有 css 程式碼錯誤
* "**pre-commit**" 在執行 git commit 前進行 lint 檢測，若不通過將拒絕提交

<h3 style="font-weight: bold;"><a id="t06">開始用 stylelint 進行編程</a></h3>

完成設定後，隨意撰寫一個 scss 樣式，即可看到 stylelint 回報的錯誤訊息

<img src="https://az787680.vo.msecnd.net/user/incredible/768eeac2-5183-4869-b725-a06acca5d1b1/1538292026_62463.png" width="300">

此時執行[上一步動作](#t03)所加入的 npm 指令碼
```bash
npm run lint
```
即可看到 command line 回報的錯誤訊息

<img src="https://az787680.vo.msecnd.net/user/incredible/768eeac2-5183-4869-b725-a06acca5d1b1/1538292414_78228.png" width="500">

接著執行自動修復的指令

```bash
npm run lint:fix
```

command line 將回報修復結果

<img src="https://az787680.vo.msecnd.net/user/incredible/768eeac2-5183-4869-b725-a06acca5d1b1/1538292375_43886.png" width="400">

樣式排序及編成風格等問題已自動修復

<img src="https://az787680.vo.msecnd.net/user/incredible/768eeac2-5183-4869-b725-a06acca5d1b1/1538292610_53263.png" width="300">

<h3 style="font-weight: bold;"><a id="t07">參考資料及相關依賴</a></h3>

[<img src="https://az788688.vo.msecnd.net/assets/img/dotblog-logo@2x.png" height="100" style="margin-right: 5px; padding: 25px;">](https://dotblogs.com.tw/explooosion/2018/09/30/141005)
[<img src="https://jes.al/public/wp-content/uploads/stylelint.png" height="150" style="margin-right: 5px;">](https://stylelint.io/)
<br/>
[Stylelint Tutorial - CSS Linter for VSCode](https://www.youtube.com/watch?v=XbMxA70ZA6o)