# Nuxt Notes

## 建立 Nuxt3 專案

步驟一. 開啟 VSCode 終端機，輸入並執行下方的指令

```bash
npx nuxi@latest init [專案名稱]
```

步驟二. 步驟一執行後會詢問是否要安裝 nuxi 套件，選擇 y 安裝

步驟三. 選擇套件管理工具。後續講解示範將會以 npm 為主，因此這邊會選擇 npm 。

步驟四. 步驟三選擇後會開始安裝 Nuxt ，安裝完畢後將會詢問是否要初始化 Git 。這邊建議初始化 Git，因此示範選擇 Yes

步驟五. 顯示 “Nuxt project has been created with the v3 template” 代表有成功建立專案，接下來就可以進入專案目錄並安裝 Nuxt3 專案的依賴套件

```bash
cd [專案名稱]
code .
```

補充 : code 是 VSCode 編輯器提供的指令。其中 code . 的用途是在當前終端機路徑下使用 VSCode 開啟該路徑中的專案資料夾。

另外需注意，MacOS 作業系統要先安裝 code 指令，才能使用 code . 指令打開專案。可以閱讀 VSCode 官方提供的  macOS 設定指南 安裝

步驟六. 在終端機執行 npm run dev 執行 dev 指令，開啟開發伺服器

```bash
npm run dev
```

## 核心檔案

app.vue : 頁面的進入點元件。

.nuxt : 由 Nuxt 框架自動生成，在開發環境用來生成 Vue，請不要刪除它、調整它。
    -如果不小心刪除，可以重跑npm run dev

tsconfig.json : TypeScript 的設定檔，預設會使用 .nuxt/tsconfig.json 的設定。
要啟用 TypeScript 需要依照 官方文件 在 nuxt.config.ts 中，設置 typescript.typeCheck: true

[官方文件](https://nuxt.com/docs/guide/concepts/typescript )

```js
// [tsconfig.json](https://nuxt.com/docs/guide/directory-structure/tsconfig)
export default defineNuxtConfig({
  typescript: {
    typeCheck: true
  }
})
```

nuxt.config.ts : Nuxt3 專案的設定檔，在初始化後預設會是 .ts 檔案 ( TypeScript ) 。詳細的設定可以至 Nuxt Configuration 查看

[官方文件](https://nuxt.com/docs/guide/concepts/typescript)

```js
// [nuxt.config.ts](https://nuxt.com/docs/guide/directory-structure/nuxt-config)
export default defineNuxtConfig({
  // compatibilityDate 屬性 : 將 Nuxt3 的功能和行為鎖定在 2024-04-03 之前的版本，
  // 避免之後 Nuxt3 新版本的寫法調整會影響到目前專案的運作
  compatibilityDate: '2024-04-03',

  // 啟用 Nuxt DevTools 開發工具
  devtools: { enabled: true }
})
```

## Nuxt 基礎指令

### nuxi init

用來初始化新的 Nuxt3 專案。

```bash
npx nuxi init [專案與資料夾名稱]
```

關於 nuxi init 指令，可以閱讀官方文件 : nuxi init

[官方文件](https://nuxt.com/docs/api/commands/init)

### nuxi add

因為 Nuxt3 預設僅提供基礎的資料夾與功能，所以在開發時需要額外使用 nuxi add 指令添加功能 ( 例如元件、路由 …等 ) 。

```bash
npx nuxi add [TEMPLATE] [NAME]
```

參數：

[TEMPLATE] : 要生成的模板名稱 ，可以填入 api 、plugin、 component、composable、 middleware、 layout,、page
[NAME] : 要生成的檔案名稱與路徑

📌 關於 nuxi add 指令，可以閱讀官方文件 : nuxi add

[官方文件](https://nuxt.com/docs/api/commands/add)

## 新增頁面

建立專案後，在 app.vue 預設會使用 < NuxtRouteAnnouncer /> 與 < NuxtWelcome /> 元件。

```vue
// app.vue

<template>
  <NuxtRouteAnnouncer />
  <NuxtWelcome />
</template>
```

📌 關於元件的用途可以閱讀官方文件 :

[< NuxtRouteAnnouncer /> 官方文件](https://nuxt.com/docs/api/components/nuxt-route-announcer)
[< NuxtWelcome /> 官方文件](https://nuxt.com/docs/api/components/nuxt-welcome)

在這一步，畫面目前顯示的是 Nuxt3 < NuxtWelcome /> 元件提供的歡迎畫面

若希望在專案可以使用自定義的頁面，需要依序執行以下兩步驟 :

  1.使用 npx nuxi add page 指令新增頁面
  2.更換 app.vue 的 < NuxtWelcome /> 元件

### npx nuxi add page 頁面名稱

產生放置頁面路由的 pages 資料夾

範例 :

```bash
// 生成　pages/index.vue ( 前台首頁 ) 　
npx nuxi add page index

// 生成　pages/admin/index.vue ( 後台首頁 )
npx nuxi add page admin/index

// 生成　pages/product/[id].vue ( 動態路由 )
// MacOS 需補上 「雙引號」，否則會出現錯誤
npx nuxi add page "product/[id]"
// Windows 無需補上 「雙引號」即可直接生成
npx nuxi add page product/[id]
```

### 使用 < NuxtPage /> 元件顯示頁面

若希望顯示 pages 資料夾新增的頁面，需要將 < NuxtWelcome /> 元件替換成 < NuxtPage />

```vue
// app.vue

<template>
  <NuxtRouteAnnouncer />
  <NuxtPage />
</template>
```

📌 關於 < NuxtPage /> 元件可以閱讀官方文件 : < NuxtPage />

[< NuxtWelcome /> 官方文件](https://nuxt.com/docs/api/components/nuxt-page)

<https://hackmd.io/JTnXov2MR4m9epBKH9VmiQ>
