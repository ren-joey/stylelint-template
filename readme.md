# STYLELINT 標準化範例

本範例參考[Robby - 全端的 Front-End Engineer](https://dotblogs.com.tw/explooosion/1) - [CSS - 運用 Stylelint 養成好習慣](https://dotblogs.com.tw/explooosion/2018/09/30/141005)所完成

### **示範環境**

本範例使用 mac 終端機<br/>
使用 [Visual Studio Code](https://code.visualstudio.com/) 進行開發

### **npm 環境建置**

使用 default 參數初始化 npm 環境

```bash
npm init -y
```

### **安裝 vscode 擴充功能**

- [stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint)<br/>
  <img src="https://az787680.vo.msecnd.net/user/incredible/768eeac2-5183-4869-b725-a06acca5d1b1/1538289428_76378.png" width="300">
- [stylefmt](https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-stylefmt)<br/>
  <img src="https://az787680.vo.msecnd.net/user/incredible/768eeac2-5183-4869-b725-a06acca5d1b1/1538289428_79332.png" width="300">
  <br/>

> 注意: 安裝完畢後須將 vscode 重新啟動

### **npm 套件安裝**

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

### **config 檔案設定**

新增 stylelint 檔案

```bash
touch stylelintrc.json
```

或者直接使用 vscode 新增該檔案

編輯檔案 _**stylelintrc.json**_

```json
{
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
            "border-top-style",
            "border-top-width",
            "border-top-color",
            "border-right-style",
            "border-right-width",
            "border-right-color",
            "border-bottom-style",
            "border-bottom-width",
            "border-bottom-color",
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
            "transition"
        ],
        "property-no-vendor-prefix": null,
        "selector-max-compound-selectors": null,
        "scss/at-import-partial-extension-blacklist": null,
        "value-no-vendor-prefix": null
      }
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

<h3 style="font-weight: bold;" id="t03"><span>新增 npm 指令</span></h3>

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

### 撰寫樣式
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

### **參考資料及依賴**
[<img src="data:image/png;base64,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" width="150" style="margin-right: 5px;">](https://dotblogs.com.tw/explooosion/2018/09/30/141005)
[<img src="https://jes.al/public/wp-content/uploads/stylelint.png" height="150" style="margin-right: 5px;">](https://stylelint.io/)
<br/>
[Stylelint Tutorial - CSS Linter for VSCode](https://www.youtube.com/watch?v=XbMxA70ZA6o)