# TT_bastion_SSH_CSV
TeraTerm MACRO for SSH connect via bastion server / SSH FORWARD LIST from hosts.csv

TeraTerm MACROを利用して、踏み台経由接続を実現する
　Windows標準SSHを利用する方式ではありません

# References  :
# 00-01_hosts.ttl (ホストリスト定義)
 SSH 接続先ホストリストを CSV から読み込み
 viewlist[], hostlist[], userlist[], element_no
 を生成する
  CSV 形式:
```
    ID,SYS_NO,HOST_TYPE,HOST_NAME,HOST_IPv4,LOGIN_USER
    "1","SP02","asterisk","test-02-01","10.nn.nn.10","username"
    "2","SP02","asterisk","test-02-02","10.nn.nn.33","username"
    "3","SP02","NFS","NFS12-01","10.nn.nn.93",""
    "4","SP02","NFS","NFS12-02","10.nn.nn.94",""
```
  ※ ダブルクォートは自動除去。末尾/先頭の空白・改行も除去。
  ※ ありがちな誤記  …  "10.nn.nn.33"."username" は "10.nn.nn.33","username" に自動修正。

# 01-00_make_forward.ttl (Port Forward確立)
  踏み台に接続し hostlist[] 全件の
  Local Port Forward をまとめて張る接続のみ。
    選択接続は01-02_connect_local.ttl 担当

# 01-01_forward_config.ttl (踏台設定)
  SSH ポートフォワード共通設定 (include)

# 01-02_connect_local.ttl (ローカル接続)
  01-00_make_forward.ttl により
  確立済みの localhost ポート群へ接続するHOSTを
  listbox で選択し Tera Term ウィンドウを開く
  !!01-00_make_forward.ttl は別途実行しておく!!

# 01-03_connect_remote.ttl (リモート接続)
  未作成

# 99-00_disconnect_all.ttl (全切断)
  未作成

# 99-01_cleanup_all.ttl (全後始末)
  未作成

# 使い方