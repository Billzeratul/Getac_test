# ==============本機檔案操作

# 查看git版本
git --version

# 初始化專案，在cmd進入專案資料夾後打入以下指令，建立一個「Git 倉庫」
git init

# 檢查狀態
git status

# 把單一檔案加入暫存區 (stage)
git add app.py

# 把全部檔案加入暫存區 (stage)
git add .

# 把單一檔案移出暫存區 (stage)
git restore --staged app.py

# 把全部檔案移出暫存區 (stage)
git restore --staged .

# 把資料夾內所有檔案加入暫存區
git add static/
git add templates/

# 把資料夾內所有檔案移出暫存區
git reset static/

# 提交 (commit)，做備註
git commit -m "新增 app.py 主程式"
git commit -m "Big Bro1"

# 查看提交紀錄 (這個常用)
git log --oneline

# gitignore，git add .時想忽略某些檔案
新增一個.gitignore檔案，並將想要忽略的檔案名稱(含副檔名)直接存入.gitignore即可
新增完後，再打入以下檔案以更新追蹤
git rm -r --cached .

# 忽略單一檔案
secret.txt
# 忽略某個資料夾
logs/
# 忽略所有 .log 檔
*.log

# ==============回到先前版本
# 回到上一個版本(回到最後一個commit的版本)
git reset --hard HEAD
# 回到上一個版本(回到上一個commit的版本)
git reset --hard HEAD~1
# 回到上一個版本(在有分支的狀態，回到上一個commit的版本，雙引號是因為^為特殊字元，避免報錯用)
git reset --hard "HEAD^1"

# 先確認上一個版本的 commit id：
git log --oneline

# 「讓 main 回到舊版本」<-我一開始用這個
1. 切回main branch
git checkout main
2. 查看提交紀錄 (看之前有甚麼版本)
git log --oneline
3. 回朔到版本471314cc，若沒有連動雲端則會刪除此版本之後的檔案
git reset --hard 471314cc
4. 上傳到GitHub，強制推送，會把本地的 main 覆蓋到遠端的 main
git push -f origin main
5. 如果反悔想要回到先前版本(快速)，使用
git reset --hard HEAD@{1}
6. 如果反悔想要回到先前版本(慢慢查)，使用
git reflog
然會會看到
abc1234 HEAD@{0}: reset: moving to v3
def5678 HEAD@{1}: commit: v5
987abcd HEAD@{2}: commit: v4
然後再使用以下指令飛回去v5版本
git reset --hard def5678

# 如果只是想「看看舊版本」
git checkout 871d4f5
動作完成後，不要直接 push，看完就切回來
git checkout main

# 如果想「在舊版本繼續開發新功能」
git checkout 871d4f5
在舊版本基礎上開一個新分支
git checkout -b new-feature-from-old
在遠端保存這條「從舊版本出發的新分支」
git push -u origin new-feature-from-old

# 回復並保留歷史（推薦）
git revert HEAD

# 回復並直接丟掉最新版本（危險 ⚠️）
git reset --hard HEAD^

# ==============上傳到GitHub

# 與遠端 (GitHub) 連線
1. 在 GitHub 建一個新的 repository，例如 Git_Test

2. 在本地專案裡設定遠端：
git remote add origin https://github.com/Billzeratul/Git_Test.git
git remote add origin https://github.com/Billzeratul/Getac_test.git

3.第一次推送，(-u的意思為)推送本地 main 到遠端 origin/main，並建立追蹤關係：
git branch -M main
git push -u origin main

之後只要(備註:git push只會push當前分支)：
git push

### 強制覆蓋遠端檔案及分支(這個超爽超好用)
git push -f origin main

### 放棄本地修改，直接同步到遠端最新版
git reset --hard origin/main

### 拉取GitHub上最新版本
git pull

# ==============狀態解釋
ca95495 (HEAD, origin/main, main) Big Bro2
藍色Head代表當前版本
紅色origin/main代表遠端版本
綠色main代表當前的branch

# ==============branch操作

# 查看提交紀錄 (這個常用)
git log --oneline

將master改為main
git branch -M main

# 建立新分支
建立分支(new-feature)
git checkout -b new-feature

切換分支
git checkout main
git checkout new-feature

合併分支
git merge new-feature

刪除分支（已合併）
git branch -d new-feature

刪除分支（尚未合併）
git branch -D new-feature

啟動遠端分支(new-feature)(前提是new-feature已被建立)
git push --set-upstream origin new-feature
刪除遠端分支(new-feature)
git push origin --delete new-feature

查看分支
git branch
# =======private加密token
⚠️ 如果你是第一次用 GitHub Private repo，GitHub 可能會要求登入或 Token：

HTTPS 模式 → 建議使用 Personal Access Token (PAT) 取代密碼。
建立方式：

GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)

我後來是用fine-grained tokens

建立一個 Token，勾選 repo 權限

推送時輸入帳號，密碼改填 Token

SSH 模式 → 可以設定 SSH key，不用每次輸入密碼。
ssh-keygen -t ed25519 -C "你的Email"
ssh-add ~/.ssh/id_ed25519

# ==============邀請協作者

如果你想讓朋友（例如 Noreen 😏）一起協作：

到 GitHub → 專案頁面 → Settings → Collaborators

輸入對方的 GitHub 帳號，送出邀請

對方接受後就能 clone 和 push。

=====================================================================
我的token
YOUR_TOKEN_HERE

# Git VScode插件
Git Graoh