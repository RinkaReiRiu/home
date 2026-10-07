# home

This is Riu's personal home page made with Google Gemini. It's also the assignment of GAI in 2026 fall.

這次作業要我設計一個自己覺得有趣且有動機製作的網頁應用程式。透過利用AI協助我從說出想像的畫面，到最後以Vibe Coding的方式，完成可實際操作的網頁。

我想要製作一個適合自己的捷徑頁面，讓我可以調整背景圖片、網站名稱、圖示和網址。比起預設的有限捷徑數量與雜亂無章的排版，畢竟是親自設計的網頁，想必會更符合自身需求。這樣一來，就能將這個頁面設為首頁，並加快我寫作業或工作的效率。

下面我參考作業要求提及的格式，依照步驟撰寫說明，並在最後揭露生成式AI的使用。

---


## 步驟一：和 AI 討論你的想法，整理出一份「規格書」。

讓我從跟AI對話開始企劃這個網頁應用程式並撰寫規格書。

- 我要撰寫一段提示詞。你必須分析我的需求，先不進行行動。等到決定所有的需求，確認完達成成就的方法，以及設立最終目標之後，你才能開始生成合適的提示詞並行動。

<img width="865" height="844" alt="image" src="https://github.com/user-attachments/assets/2cf3e8bc-ec42-4fb9-9272-b1d7c47e347a" />

<img width="865" height="414" alt="image" src="https://github.com/user-attachments/assets/5ef50ed5-6244-4c36-b613-c750368bcba3" />

<img width="865" height="373" alt="image" src="https://github.com/user-attachments/assets/51048212-e634-4208-9678-f38ce40ab941" />

<img width="865" height="694" alt="image" src="https://github.com/user-attachments/assets/2d5fb013-e862-47ec-92a7-c3a9da642e0c" />

<img width="865" height="528" alt="image" src="https://github.com/user-attachments/assets/7a3a2341-fbb6-47c5-8402-40b9af95ac90" />

我希望可以自行上傳背景圖片，背景圖片會霧化處理；自動取得捷徑圖示；此網頁必須適用於所有裝置，依照畫面大小及比例自動適配性調整。我希望網頁本身具備新增、編輯、刪除按鈕的功能，具備三個頁籤（學校作業、工作工具、休閒娛樂），且可以跨裝置聯動更改畫面；所有的網址、網頁簡稱以獨立的csv檔案儲存，讓我可以輕鬆新增並編輯。我希望輸入給LLM時，它能生成完整且無錯誤的單一整合檔及獨立csv檔案。

然而，基於資訊安全限制，前端JavaScript無法直接「靜默修改並覆寫」您電腦或手機裡的本地端 csv 檔案；若只是讀取本地檔案，也無法憑空達成所謂的「跨裝置聯動」。為了完全透過Vibe Coding交給LLM完成能運作的程式碼，我決定讓AI新增一個匯入、匯出csv的功能，可用於備份和轉移至其他裝置。

以下是LLM初步生成的提示詞。

```

# 角色設定
你是一位資深前端工程師 (Senior Front-end Engineer)，精通 HTML5, CSS3, 現代化原生 JavaScript (Vanilla JS)，以及精美的 UI/UX 設計（特別是玻璃擬物化 Glassmorphism 與自適應設計 RWD）。

# 任務目標
請為我開發一個「個人化捷徑首頁 (Personal Dashboard)」。
為了方便部署，請將所有的 HTML, CSS, JavaScript 全部寫在「單一個 .html 檔案」中，並額外提供一份「預設的 .csv 檔案」格式範例。

# 核心功能與介面需求
1. 視覺與佈局 (UI & Layout)：
   - 採用毛玻璃風格 (Glassmorphism)，包含半透明的卡片設計與柔和的陰影。
   - 支援自適應網頁設計 (Responsive Web Design)，確保在手機、平板與桌機上皆能完美顯示（推薦使用 CSS Grid 或 Flexbox）。
   - 頁面主體分為三個頁籤 (Tabs)：「學校作業」、「工作工具」、「休閒娛樂」。使用者可以點擊切換不同類別的捷徑。

2. 背景圖片管理 (Background Management)：
   - 網頁需提供「上傳背景圖片」的按鈕。
   - 背景圖片需進行霧化處理（可使用 CSS `backdrop-filter: blur()` 或遮罩）。
   - 透過 JavaScript 將上傳的圖片轉為 Base64 格式，並儲存於瀏覽器的 LocalStorage 中，確保下次開啟時維持相同背景。

3. 捷徑卡片設計 (Shortcut Cards)：
   - 每個捷徑卡片需顯示：網站名稱、網址、以及網站圖示。
   - **自動圖示抓取**：請撰寫邏輯，利用 Google Favicon API 自動獲取捷徑圖示（例如：`https://s2.googleusercontent.com/s2/favicons?domain={網址}&sz=128`）。

4. 資料庫與互動邏輯 (Data & CRUD Operations)：
   - 網頁內必須具備「新增 (Add)」、「編輯 (Edit)」、「刪除 (Delete)」捷徑的 UI（例如彈出式視窗 Modal）。
   - 所有捷徑資料預設必須即時儲存在瀏覽器的 LocalStorage 中。
   - 資料結構必須包含：ID, 名稱, 網址, 所屬分類 (Tab)。

5. 跨裝置聯動解決方案 (CSV Import/Export)：
   - 實作「匯出 CSV」功能：將目前 LocalStorage 裡的捷徑資料打包成 CSV 下載。
   - 實作「匯入 CSV」功能：使用者可上傳 CSV，JavaScript 需解析該 CSV 並覆寫 LocalStorage 的資料，隨即重新渲染畫面。
   - CSV 欄位規範：`category, name, url`。

# 輸出要求
1. 請先簡短說明你的設計思維。
2. 產出完整的單一 `index.html` 程式碼（包含 `<style>` 與 `<script>`）。程式碼必須無錯且可直接在瀏覽器雙擊運行。
3. 產出一份名為 `shortcuts.csv` 的純文字內容，作為匯入格式的範例。

```

---


## 步驟二：根據規格書，利用 Vibe Coding 完成網頁。

我將這份提示詞重新輸入至Google Gemini Pro延伸模型，要求開始生成程式碼。

AI根據我提供的規格書，讓我透過Vibe Coding完成第一版的程式碼，包含一HTML整合檔和一csv檔案。HTML程式碼用於網站設計與互動功能，csv檔案彙整了所有的網站名稱、網址和分類。

<img width="865" height="841" alt="image" src="https://github.com/user-attachments/assets/8ba6cea4-ba02-4cc4-9908-88d411d7bf65" />

我跟AI說沒有完整顯示出csv檔的所有網址，其他部分測試過後沒有發現問題。意外的只有這一個小錯誤。

<img width="865" height="377" alt="image" src="https://github.com/user-attachments/assets/d3dcf19d-d8bc-4c14-8c9d-e13790a62952" />

這是預設的網站頁面。

<img width="865" height="563" alt="image" src="https://github.com/user-attachments/assets/63154915-0ef7-4d63-9a02-4910993b5c92" />
 
預設的網站頁面背景圖片來源為Unsplash圖庫，為免費商用授權圖片。

<img width="865" height="567" alt="image" src="https://github.com/user-attachments/assets/12fd4804-22b7-4039-a70c-a7f1be2acde9" />

上傳背景圖片後的實際上畫面如下圖。這張圖片是我的自拍照。

<img width="865" height="563" alt="image" src="https://github.com/user-attachments/assets/b35046e8-aef4-4188-bd7f-6fc91115de41" />

還可以在頁面上新增捷徑，並匯出csv備份自己的設置到其他裝置。

<img width="509" height="597" alt="image" src="https://github.com/user-attachments/assets/789f8a85-076d-4e35-9f56-e79cb3eb858e" />

<img width="865" height="319" alt="image" src="https://github.com/user-attachments/assets/ffef91f0-1ffb-472f-9164-483fa7a54299" />

<img width="850" height="242" alt="image" src="https://github.com/user-attachments/assets/bf17a1ac-d615-4777-acfa-17178e7267bb" />

---


## 步驟三：將作品上傳到 GitHub，並使用 GitHub Pages 公開網站。

最後，只要上傳到GitHub並公開就完成了。

<img width="850" height="242" alt="image" src="https://github.com/user-attachments/assets/f6e814e6-3307-47df-ad37-efe9eb2d6623" />
 
GitHub Repo： [https://github.com/RinkaReiRiu/home/](https://github.com/RinkaReiRiu/home/)

GitHub Pages： [https://rinkareiriu.github.io/home/](https://rinkareiriu.github.io/home/)

---


## 結論

每個人一開始點進來會是預設的頁面，可以自行編輯更改後，匯出csv檔案備份，本身也會儲存到瀏覽器暫存內。雖然我做的是給我自己使用的首頁，但如果其他人想用的話，也能同時按照自己的習慣使用。

---


## 生成式AI揭露

本次作業採Google Gemini協作完成企劃，撰寫規格書；以Vibe Coding的形式完成網頁設計。詳細過程請見文內詳細步驟。其中，部分步驟有修改AI的文字敘述，簡略解說步驟過程，以避免文章篇幅太過冗長。

---

