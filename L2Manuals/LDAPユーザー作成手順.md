<p><strong>◇Redmineユーザー作成手順</strong><br>

<p><font color="SeaGreen">1,踏み台サーバ(sandbox5:10.184.199.7)にリモートデスクトップログイン</font><br>
<strong>！要VPN接続</strong><br>
<p>□接続情報<br>
<font color="Lime">・IP:10.184.199.7<br>
・ID:各自に払い出されたID<br>
・PW:各自に払い出されたパスワード</font><br>

<p><font color="SeaGreen">2,踏み台サーバーにてTeraTermでsandobx環境にSSHログイン</font><br>
<p>□接続情報<br>
<font color="Lime">・sanndboxサーバーIP：10.184.235.37<br>
・ユーザ名：ec2-user<br>
・パスフレーズ：なし<br>
・秘密鍵：ec2-user.pem</font><br>

<p><font color="SeaGreen">3,必要なファイルが配置されたディレクトリを複製</font><br>
<font color="Crimson"># cp -Rp /home/zenke /home/[ユーザーID]</font><br>

<p>・必要なファイル<br>
<font color="Lime">/home/zenke/users.txt<br>
/home/zenke/template.ldif<br>
/home/zenke/create_ldif</font><br>

<p>・必要なディレクトリ<br>
<font color="Lime">/home/zenke/key_pairs<br>
/home/zenke/ldifs</font><br>

<p><font color="SeaGreen">4,以下コマンドを実行しユーザーに設定するUIDを取得</font><br>
<font color="Crimson"># ldapsearch -LLL -h mng01-a-tky-ldap-master-common.aws.fastretailing.com -x -b "dc=aws,dc=fastretailing,dc=com" "(objectClass=*)" uidNumber | grep uidNumber | awk '{print $2;}' | sort -n|tail</font><br>

<p>▽以下実行例<br>
<font color="Maroon">[root@mng01-a-tky-infra-sandbox2 s_fukusaka]# ldapsearch -LLL -h mng01-a-tky-ldap-master-common.aws.fastretailing.com -x -b "dc=aws,dc=fastretailing,dc=com" "(objectClass=*)" uidNumber | grep uidNumber | awk '{print $2;}' | sort -n|tail<br>
6033<br>
6034<br>
6035<br>
6036<br>
6037<br>
6038<br>
6039<br>
6040<br>
6041</font><br>

<p><strong>！現在使用されているUIDの値が出力されるので一番下の値に+1したものをメモ帳等に保存</strong><br>

<p><font color="SeaGreen">5,users.txtを編集</font><br>
<font color="Crimson"># vi /home/[ユーザーID]/users.txt</font><br>

<p>※半角スペース区切りにて[UID] [イニシャル] [ユーザーID] [名] [姓] [メールアドレス]<br>の順に記載する<br>

<p>□以下記載例<br>
--------------------------------------------------------------------------<br>
<font color="Maroon">6042 HK hitoshi.koyanagi hitoshi koyanagi koyanagiht@nttdata.co.jp</font><br>
--------------------------------------------------------------------------<br>

<p><strong>！UIDは<font color="SteelBlue">"4,"</font>の例では6041なので+1した6042を使用</strong><br>

<p><font color="SeaGreen">6,秘密鍵生成</font><br>
6-1 コマンドにて秘密鍵生成<br>▽実行コマンド例<br>
<font color="Crimson"># cd /home/[ユーザーID]/</font><br>
<font color="Crimson"># ssh-keygen -t rsa -f [ユーザーID].key -C "メールアドレス"</font><br>
※パスワードを聞かれるが入力なし(Enter)でOK<br>

<p>▽以下実行例<br>
<font color="Maroon">[root@mng01-a-tky-infra-sandbox2 yoshito.nodagashira]# ssh-keygen -t rsa -f yoshito.nodagashira.key -C "nodagashira@nnetworks.co.jp"<br>
Generating public/private rsa key pair.<br>
Enter passphrase (empty for no passphrase):yoshito.nodagashira<br>
Enter same passphrase again:yoshito.nodagashira
Your identification has been saved in yoshito.nodagashira.key.<br>
Your public key has been saved in yoshito.nodagashira.key.pub.<br>
The key fingerprint is:
ea:6a:6a:56:20:97:45:df:f9:9d:a1:6e:82:16:98:09 nodagashira@nnetworks.co.jp<br>
The key's randomart image is:<br>
+--[ RSA 2048]----+<br>
|   ..            |<br>
|    .. . .       |<br>
|  Eo  . o   .    |<br>
|. +. +   . o o   |<br>
| o .+ . S o o    |<br>
|    .  + .       |<br>
|   .  + . o      |<br>
|  o .o   o       |<br>
| o.o...          |<br>
+-----------------+</font><br>

<p>6-2<br>
作成したファイルを移動及びリネーム<br>
<font color="Crimson"># mv [ユーザーID].key.* ./key_pairs/</font><br>
<font color="Crimson"># cd ./key_pairs</font><br>
<font color="Crimson"># mv [ユーザーID].key.pub [ユーザーID].pub</font><br>

<p><font color="SeaGreen">7,LDAPサーバにログインし、パスワードを設定し暗号化したものを取得</font><br>
・sandboxサーバ(10.184.235.37)にてrootになり鍵を使ってLDAPサーバーにログイン<br>
<font color="Crimson"># sudo su -</font><br>
<font color="Crimson"># ssh -i /root/fr-admin.pem fr-admin@10.184.232.8</font><br>

<p>▽実行コマンド例<br>
<font color="Crimson"># slappasswd -h {SSHA} -s [ランダム文字列英数8文字]</font><br>
<font color="Maroon">{SSHA}****************************</font><br>
のようなハッシュ化された値が出力されるのでメモ帳等に控えておく<br>

<p><font color="SeaGreen">8,sandboxサーバーに戻りスクリプトを使用してLDAP用インポートファイルを作成</font><br>
<font color="Crimson"># sh /home/ユーザーID/create_ldif /home/[ユーザーID]/user.txt</font><br>

<p><font color="SeaGreen">9,踏み台サーバー(sandbox5:10.184.199.7)にてLDAPadminを使用して所属するグループのGIDを取得</font><br>
□LDAPadmin接続先及び入力情報<br>
<font color="Lime">・サーバーIP：10.184.232.8<br>
・Base: dc=aws,dc=fastretailing,dc=com<br>
・ユーザ名：dc=aws,dc=fastretailing,dc=com<br>
・パスフレーズ：00Xh3Iup</font><br>

<p><font color="SteelBlue">"ou=Group"</font>をクリックし、対象ユーザーのメールアドレスのドメイン部分を探し、右クリックし<font color="SteelBlue">"Edit entry"</font>をクリックし<font color="SteelBlue">"gidNumber"</font>の値をメモ帳等に保存<br>

<p><font color="SeaGreen">10,sandboxサーバーに戻り生成されたインポートファイルを編集</font><br>
<font color="Crimson"># vi /home/[ユーザーID]/ldifs/[ユーザーID].ldif</font><br>

<p>値のうち<br>
<font color="SteelBlue">"gidNumber: "</font>に<font color="SteelBlue">"9,"</font>で取得した値、と<font color="SteelBlue">"userPassword: "</font>に<font color="SteelBlue">"7,"</font>で取得した値を入力<br>

<p><strong>！userPassword:と{SSHA}の間に空白スペースを入れるようにして下さい</strong><br>

<p><font color="SeaGreen">11,winscpを使用してsandboxサーバーからldifファイルを取得</font><br>
<font color="Lime">・sanndboxサーバーIP：10.184.235.37<br>
・ユーザ名：ec2-user<br>
・パスフレーズ：なし<br>
・秘密鍵：ec2-user.ppk</font><br>

<p>・コピー元ldif保存場所<br>
/home/ユーザーID/ldifs/ユーザーID.ldif<br>

<p><strong>※10で編集したものをデスクトップに保存</strong><br>

<p><font color="SeaGreen">12,LDAPadminにて<font color="SteelBlue">"ou=People"</font>を確認し、追加するユーザー名が既に使用されていないか確認する</font><br>

<p><font color="SeaGreen">13,存在していなければ<font color="SteelBlue">"tools"</font>→<font color="SteelBlue">"import"</font>をクリックし、踏み台サーバー上のデスクトップの[ユーザーID.ldif]ファイルを選択しimport</font><br>

<p><font color="SeaGreen">14,<font color="SteelBlue">"9,"</font>で確認したグループにユーザーを追加</font><br>

<p><font color="SteelBlue">"Ou=Group"</font>の対象グループを右クリックし<font color="SteelBlue">"Edit entry"</font>をクリック<br>
1番下までスクロールし、プルダウンメニューの<font color="SteelBlue">"member"</font>をクリックし[ユーザーID]を入力しフロッピーディスクマークをクリックし保存<br>

<p><strong>！！！！こちらで完了となります！！！！</strong><br>


<p>追加手順<br>
<p>1,openVPNも追加する必要がある場合</font><br>
LDAPadminにて<br>
<font color="SteelBlue">"Ou=ServiceGroup"</font>→<font color="SteelBlue">"ou=VPN"</font>→<font color="SteelBlue">"cn=Consumer"</font>の順で選択し<br>
<font color="SteelBlue">"cn=Consumer"</font>を右クリックして<font color="SteelBlue">"Edit entry"</font>をクリックし
1番下までスクロールし、プルダウンメニューの<font color="SteelBlue">"member"</font>をクリックし<br>
<font color="SteelBlue">"uid=[ユーザーID],ou=People,dc=aws,dc=fastretailing,dc=com"</font><br>
を入力しフロッピーディスクマークをクリックし保存<br>

<p>2,redminにladp連携する必要がある場合redminにてユーザー作成をする際に
<font color="SteelBlue">"認証方式"</font>にて<font color="SteelBlue">"ldap"</font>を選択して下さい<br>

<p>3,jenkins認証がある場合にはLDAPadminを使用し、指定されているjenkinsのldapグループに<font color="SteelBlue">"14,"</font>の手順にて追加して下さい<br>