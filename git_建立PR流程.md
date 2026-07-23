# 第一步：使用 CLI 將專案抓到電腦裡
開啟你的命令提示字元 (Command Prompt)，輸入以下指令將雲端的程式碼「複製」一份到本機：
git clone https://github.com/你的帳號/專案名稱.git
cd 專案名稱

# 第二步：建立新分支 (Branch)
在開發新功能時，我們會習慣開一個獨立的「小房間」，不要直接在主線（main）修改：
git checkout -b feature-update-readme

# 第三步：修改檔案並提交 (Commit)
你可以用記事本或 VS Code 修改檔案。改完後，回到 CLI 告訴 Git 你做了什麼：

暫存變更： git add .

標記訊息： git commit -m "修正了說明文件的錯字"

# 第四步：上傳並開啟 PR
將你的小房間（分支）推送到雲端 GitHub：
git push origin feature-update-readme

# 第五步：在 GitHub 網頁操作
這時候，當你打開 GitHub 網頁，你會看到一個黃色的提示框寫著 "Compare & pull request"。

點擊按鈕。

寫下你改了什麼（例如：我修復了第 10 行的語法錯誤）。

按下 Create pull request。
# ===================Merge分支========================
# 方法1. 最直覺的方式：透過 GitHub 網頁介面 (推薦)
這是大多數團隊使用的做法，因為它有完整的視覺紀錄。

步驟一： 進入該 PR 的頁面。

步驟二： 捲動到頁面下方，你會看到一個大大的綠色按鈕 "Merge pull request"。

步驟三： 點擊後，系統會讓你輸入合併訊息（通常預設即可），再點擊 "Confirm merge"。

# 方法2. 進階玩家：透過 CLI (命令提示字元) 手動合併
如果你偏好在終端機操作，或者需要處理複雜的衝突，可以手動執行：

切換回主要分支：
git checkout main

拉取雲端最新的狀態：
git pull origin main

將開發分支（例如 feature-update）合併進來：
git merge feature-update

推送到雲端：
git push origin main

Gemini 說了
身為專案管理者，當你收到成員的 PR (Pull Request) 並確認程式碼沒問題後，通常有兩種主要方式可以將這些變更合併到主要分支（通常是 main 或 master）。

1. 最直覺的方式：透過 GitHub 網頁介面 (推薦)
這是大多數團隊使用的做法，因為它有完整的視覺紀錄。

步驟一： 進入該 PR 的頁面。

步驟二： 捲動到頁面下方，你會看到一個大大的綠色按鈕 "Merge pull request"。

步驟三： 點擊後，系統會讓你輸入合併訊息（通常預設即可），再點擊 "Confirm merge"。

2. 進階玩家：透過 CLI (命令提示字元) 手動合併
如果你偏好在終端機操作，或者需要處理複雜的衝突，可以手動執行：

切換回主要分支：

Bash
git checkout main
拉取雲端最新的狀態：

Bash
git pull origin main
將開發分支（例如 feature-update）合併進來：

Bash
git merge feature-update
推送到雲端：

Bash
git push origin main
# 管理者常見的三種合併選項
在點擊 GitHub 上的綠色按鈕旁，通常會有一個小箭頭，讓你可以選擇不同的合併策略：

# 合併方式
Create a merge commit	保留所有的提交歷史，並產生一個新的「合併提交」。	優點: 最完整的開發歷史。

Squash and merge	將對方的多個小提交「壓縮」成一個大的提交再合併。	優點: 讓主分支的歷史紀錄看起來非常乾淨。

Rebase and merge	將對方的提交直接接在主分支的最後面。	優點: 線性歷史，不會產生額外的 Merge 節點。

小撇步： 合併完成後，GitHub 通常會提示你 "Delete branch"。建議養成習慣把已經合併的分支刪除，這樣專案的結構才不會越來越亂。