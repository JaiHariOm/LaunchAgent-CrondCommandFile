# LaunchAgent & cron での自動化

### きっかけ

* mac os sierra へのアップグレードで,brew fileの自動化を設定していた cron の /ver/mail/user への出力が来なくなり、その原因を調べている過程で cron 及び LaunchAgent のことを改めて学ぶことになった。

### 結果

* 色々と試行錯誤していった結果
    * cron の /ver/mail/user への出力ができるように設定できた
    * LaunchAgent の設定ができるようになった
    * rsync というコマンドで監視とコピー、同期ができるようになった
    
## cron の実行と /ver/mail/user への出力設定

* 任意の場所にフォルダーを作り、そこにはコマンド実行ファイルを格納、そのファイルを cron で実行
* log の出力はデフォルトでは、何ら設定しなくても出力されるはずなのだが、改めて cron → sendmail などで検索し設定方法調べてみた
* iTarm(ターミナル)→vim→crontab で、MAILTO=username@USERNAME.local と追加することで設定できることがわかったが、何度試しても crontad へ追記保存できない状態
* そこで rootuser を設定して直接ファイルを開いて編集、保存
* テストの結果、log が/ver/mail/user へ出力されるようになった

 

## LaunchAgent plistFile 設定

* cron と同じく brew file で Homebrew のアップデートを設定してみる
* brew cask の upgrade も設定する
    * 苦労したのは、実行コマンドへの PATH と 実行コマンド及びオプションの書き方

## 結果通知コマンド terminal-notifier

* brew file コマンドの実行後に実行するよう指定したもう一つのコマンド terminal-notifier は、コマンド実行が成功した場合に指定したメッセージを通知センターで知らせるというもの

## rsync でのBackUp

* rsync コマンドとは、指定したフォルダーやファイルの変更や編集を別ディレクトリへ自動で同期や変更の差分が追加コピーするためのコマンド
* /tmp/ へ出力される log は、パソコンをシャットダウンするとリセットされるので、BackUp をする設定を launcd に設定した


## まとめ

何となく今のところはうまく行っているような気がするが、設定方法などまだまだ研究の余地はあると思うので、もう少し探っていこうと思っていいる
