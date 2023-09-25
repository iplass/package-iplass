<a id="english"></a>
#### English ( [日本語](#japanese) )

## About iPLAss
iPLAss is a java-based enterprise class low-code web development platform, which have been focused on boosting the productivity of system development.  
MVC based framework with non-programming development mechanism ensure both Productivity and Customizability.

**<a href="https://iplass.org/en/" target="_blank">iPLAss Official Site</a>**

## Image
iPLAss's docker image for the Web server bundled with Tomcat.  
To have it run in practice, the supported Database and corresponding JDBC driver is required.

## Volume
`/var/lib/iplass` (IPLASS_HOME)  
The home directory for iPLAss, where the definition file and JDBC driver suppose to be placed at.

## Prerequisite
1. Create the mount directory for IPLASS_HOME.
Please also host the mount directory.

1. Install JDBC driver
At the hosting mount directory created above, create directory named `jdbc`, and place the corresponding JDBC driver's jar file to `jdbc` directory.


## Booting
There are two ways to boot up, the "direct booting" and the "installer booting".

### Direct booting
"direct booting" is the way of boot up to utilize existed iPLAss database and service-config file without using the installer. 

#### prepare for booting  
Place the service-config file: 'iplass-service-config.xml' to the hosting mount directory.  
If there does not exist such a service-config file, then the "installer booting" should be chosen.

※If the user want to rename the service-config file other than  "iplass-service-config.xml", then it is necessary to specify it by Java's system property 'mtp.config'.  
Example: if the service-config file is renamed to `my-service-config.xml` and is placed at `IPLASS_HOME/conf`.

	docker run -e CATALINA_OPTS='-Dmtp.config=$IPLASS_HOME/conf/my-service-config.xml' ・・・

#### Environment Variables
##### 3.1.36 or later, 3.2.11 or later versions
If you are using 3.1.36 or later or 3.2.11 or later versions, the following environment variables are available.  
If a reverse proxy is applied to your environment, please change the proxy-related settings accordingly.

- `TOMCAT_CONNECTOR_HTTP_PORT`  
  default value: `8080`  
  Set the `port` attribute of the http connector element in ${CATALINA_HOME}/conf/server.xml.
- `TOMCAT_CONNECTOR_HTTP_CONNECTION_TIMEOUT`  
  default value: `20000`  
  Set the `connectionTimeout` attribute of the http connector element in ${CATALINA_HOME}/conf/server.xml.
- `TOMCAT_CONNECTOR_HTTP_REDIRECT_PORT`  
  default value: `8443`  
  Set the `redirectPort` attribute of the http connector element in ${CATALINA_HOME}/conf/server.xml.
- `TOMCAT_CONNECTOR_HTTP_MAX_PARAMETER_COUNT`  
  default value: `1000`  
  Set the `maxParameterCount` attribute of the http connector element in ${CATALINA_HOME}/conf/server.xml.
- `TOMCAT_CONNECTOR_HTTP_PROXY_NAME`  
  default value: none  
  Set the `proxyName` attribute of the http connector element in ${CATALINA_HOME}/conf/server.xml.
- `TOMCAT_CONNECTOR_HTTP_PROXY_PORT`  
  default value: none  
  Set the `proxyPort` attribute of the http connector element in ${CATALINA_HOME}/conf/server.xml.
- `TOMCAT_CONNECTOR_HTTP_SCHEME`  
  default value: `http`  
  Set the `scheme` attribute of the http connector element in ${CATALINA_HOME}/conf/server.xml.
- `TOMCAT_CONNECTOR_HTTP_SECURE`  
  default value: `false`  
  Set the `secure` attribute of the http connector element in ${CATALINA_HOME}/conf/server.xml.

##### 3.0.10 or older versions
for 3.0.10 or older versions, it is necessary to specify the following environment variables in command lines.

- IPLASS_DB_TYPE (required)  
Specify the type of the Database.  
Please specify one of the following Database
  - 'MySQL'  
Use this command when using 'MySQL'.
  - 'Oracle_EE_11g'  
Use this command when using 'Oracle Database 11g'.
  - 'Oracle_EE_12c'  
Use this command when using 'Oracle Database 12c'.
  - 'Oracle_SE_ONE'  
Use this command when using 'Oracle Database Standard Edition'.
  - 'PostgreSQL'  
Use this command when using 'PostgreSQL'.
  - 'SQLServer'  
Use this command when using 'Microsoft SQL Server'.

- IPLASS_DB_CONN (required)  
Specify the method of connection to the Database.  
The method of connection to the Database can be one of the followings. It is recommended to use 'DataSource'.
  - 'DataSource'  
Use this command when using 'DataSource' as the method of connection.
  - 'DriverManager'  
Use this command when using 'DriverManager' as the method of connection.

- IPLASS_DS_NAME (only required when DataSource was specified above)  
Declare the name of the DataSource.

- IPLASS_JDBC_DRIVER_CLASS (optional)  
Specify the JDBC class name.  
If not specified, the corresponding JDBC class is chosen based on the given Database.

- IPLASS_JDBC_HOST (required)  
Specify the host name or IP address of the Database.

- IPLASS_JDBC_PORT (optional)  
Specify the port number for the Database.  
If not specified, the default port is set based on the given Database.

- IPLASS_JDBC_SERVICE_NAME (only required when Oracle was specified above)  
specify the service name of the Database.

- IPLASS_JDBC_URL (optional)  
Specify the JDBC's connection URL.  
If not specified, the default URL is chosen based on the given Database.

- IPLASS_JDBC_USER (required)  
Specify the database user's username for iPLAss.

- IPLASS_JDBC_PASSWORD (required)  
Specify the database user's password for iPLAss.

### Installer booting
"installer booting" is the way of booting when it is the first time to use iPLAss.  
The installer page will be presented at first access.

"installer booting" does not require any preparation and environment variables.

### Command to start
	docker run -p 8080:8080 -v [IPLASS_HOME's mount directory]:/var/lib/iplass ghcr.io/iplass/iplass

## How to use
Once the container was initiated, please access the following URL at your web browser.
- for direct booting  
<a href="http://localhost:8080/iplass/[TenantName]/gem/" target="_blank">http://localhost:8080/iplass/[TenantName]/gem/</a>
- for installer booting  
<a href="http://localhost:8080/iplass" target="_blank">http://localhost:8080/iplass</a>

<a id="japanese"></a>
#### 日本語 ( [English](#english) )

## iPLAssについて
iPLAssとは、エンタープライズクラスのシステム開発における生産性向上を主目的とした、javaベースの開発プラットフォームです。  
MVCパターンベースの開発フレームワーク上にノンプログラミングでの開発を可能とする機能を提供し、高い生産性とカスタマイズ性を両立させます。

**<a href="https://iplass.org/" target="_blank">iPLAssオフィシャルサイト</a>**

## イメージ
WebサーバにTomcatをバンドルしたiPLAssのDockerイメージです。  
動作には別途iPLAssに対応したデータベースとJDBCドライバが必要です。

## ボリューム
`/var/lib/iplass` (IPLASS_HOME)  
iPLAssのホームディレクトリです。定義ファイルやJDBCドライバなどを配置します。

## 事前準備
1. IPLASS_HOMEのマウントディレクトリ作成  
IPLASS_HOMEにマウントするディレクトリをホストに作成してください。

1. JDBCドライバのインストール  
ホストに作成したIPLASS_HOMEのマウントディレクトリに`jdbc`ディレクトリを作成し、使用するデータベースのJDBCドライバのJARファイルを`jdbc`ディレクトリに配置してください。

## 起動
起動には「ダイレクト起動」と「インストーラ起動」の二通りの方式があります。

### ダイレクト起動
「ダイレクト起動」は既存のiPLAssデータベースとservice-configファイルを使用しインストーラを介さずにダイレクトに起動する方式です。

#### 起動準備  
ホストに作成したIPLASS_HOMEのマウントディレクトリにservice-configファイル「iplass-service-config.xml」を配置してください。  
service-configファイルが存在しない場合は「インストーラ起動」となります。

※service-configファイルのファイル名を`iplass-service-config.xml`以外とする場合はJavaのシステムプロパティ`mtp.config`による指定が必要です。  
指定例：service-configファイルのファイル名を`my-service-config.xml`として`IPLASS_HOME/conf`に配置する場合

	docker run -e CATALINA_OPTS='-Dmtp.config=$IPLASS_HOME/conf/my-service-config.xml' ・・・

#### 環境変数 
##### 3.1.36 以降、3.2.11 以降 のバージョン
3.1.36 以降、3.2.11 以降のバージョンを利用している場合は、以下の環境変数を利用することが可能です。  
リバースプロキシが適用されている環境の場合はプロキシに関連する設定を適宜変更ください。

- `TOMCAT_CONNECTOR_HTTP_PORT`  
  デフォルト値: `8080`  
  ${CATALINA_HOME}/conf/server.xml の http connector 要素の `port` 属性を設定します。
- `TOMCAT_CONNECTOR_HTTP_CONNECTION_TIMEOUT`  
  デフォルト値: `20000`  
  ${CATALINA_HOME}/conf/server.xml の http connector 要素の `connectionTimeout` 属性を設定します。
- `TOMCAT_CONNECTOR_HTTP_REDIRECT_PORT`  
  デフォルト値: `8443`  
  ${CATALINA_HOME}/conf/server.xml の http connector 要素の `redirectPort` 属性を設定します。
- `TOMCAT_CONNECTOR_HTTP_MAX_PARAMETER_COUNT`  
  デフォルト値: `1000`  
  ${CATALINA_HOME}/conf/server.xml の http connector 要素の `maxParameterCount` 属性を設定します。
- `TOMCAT_CONNECTOR_HTTP_PROXY_NAME`  
  デフォルト値: 無し  
  ${CATALINA_HOME}/conf/server.xml の http connector 要素の `proxyName` 属性を設定します。
- `TOMCAT_CONNECTOR_HTTP_PROXY_PORT`  
  デフォルト値: 無し  
  ${CATALINA_HOME}/conf/server.xml の http connector 要素の `proxyPort` 属性を設定します。
- `TOMCAT_CONNECTOR_HTTP_SCHEME`  
  デフォルト値: `http`  
  ${CATALINA_HOME}/conf/server.xml の http connector 要素の `scheme` 属性を設定します。
- `TOMCAT_CONNECTOR_HTTP_SECURE`  
  デフォルト値: `false`  
  ${CATALINA_HOME}/conf/server.xml の http connector 要素の `secure` 属性を設定します。

##### 3.0.10以前のみ  
3.0.10以前を利用の場合は、起動コマンドに以下の環境変数の指定が必要です。

- IPLASS_DB_TYPE (必須)  
データベースの種類を指定します。  
データベースの種類は以下のいずれかを指定してください。
  - 'MySQL'  
「MySQL」を使用する場合に指定します。
  - 'Oracle_EE_11g'  
「Oracle Database 11g」を使用する場合に指定します。
  - 'Oracle_EE_12c'  
「Oracle Database 12c」を使用する場合に指定します。
  - 'Oracle_SE_ONE'  
「Oracle Database Standard Edition」を使用する場合に指定します。
  - 'PostgreSQL'  
「PostgreSQL」を使用する場合に指定します。
  - 'SQLServer'  
「Microsoft SQL Server」を使用する場合に指定します。

- IPLASS_DB_CONN (必須)  
データベースの接続方式を指定します。  
データベースの接続方式は以下のいずれかを指定します。接続方式は'DataSource'を推奨します。
  - 'DataSource'  
データソースを使用して接続する場合に指定します。
  - 'DriverManager'  
ドライバマネージャを使用して接続する場合に指定します。

- IPLASS_DS_NAME (データベースの接続方式が'DataSource'の場合にのみ必須)  
データソース名を指定します。

- IPLASS_JDBC_DRIVER_CLASS (任意)  
JDBCドライバのクラス名を指定します。  
省略時は指定されたデータベースの種類により自動的に設定されます。

- IPLASS_JDBC_HOST (必須)  
データベースのホスト名またはIPアドレスを指定します。

- IPLASS_JDBC_PORT (任意)  
データベースのポート番号を指定します。  
省略時は設定されたデータベースの種類により自動的に設定されます。

- IPLASS_JDBC_SERVICE_NAME (データベースの種類がOracleの場合にのみ必須)  
データベースのサービス名を指定します。

- IPLASS_JDBC_URL (任意)  
JDBCの接続URLを指定します。  
省略時は設定されたデータベースの種類により自動的に設定されます。

- IPLASS_JDBC_USER (必須)  
iPLAssのデータベースユーザのユーザ名を指定します。

- IPLASS_JDBC_PASSWORD (必須)  
iPLAssのデータベースユーザのパスワードを指定します。

### インストーラ起動
「インストーラ起動」は新規にiPLAssを使用する場合の起動方式です。  
初回アクセス時にiPLAssのインストーラ画面が表示されます。

「インストーラ起動」では特別な起動準備や環境変数の指定は必要ありません。

### 起動コマンド
	docker run -p 8080:8080 -v [IPLASS_HOMEのマウントディレクトリ]:/var/lib/iplass ghcr.io/iplass/iplass

## 使用方法
コンテナ起動後、Webブラウザで次のURLにアクセスしてください。
- ダイレクト起動の場合  
<a href="http://localhost:8080/iplass/[テナント名]/gem/" target="_blank">http://localhost:8080/iplass/[テナント名]/gem/</a>
- インストーラ起動の場合  
<a href="http://localhost:8080/iplass" target="_blank">http://localhost:8080/iplass</a>