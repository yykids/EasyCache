## Database > EasyCache > リリースノート

### 2020. 03. 24.

#### 機能改善

- EasyCache基本設定値の変更（tcp-keepalive[0→300]）

### 2020. 02. 25.

#### 機能改善
- 接続情報を同時に複数個を追加ができるように修正
- SMS内容改善
- 重複されたCIDRを入力した際のメッセージ修正

#### バグ修正
- 大容量データがある際、Replicaノードを追加する場合データの同期化が無限ループが発生する問題を修正
- レプリケーショングループでノードの作成が失敗した際、ノードの一覧で作成中の表示が消えずに表示されている問題を修正

### 2020. 02. 11.

#### 機能改善

- TOAST認証モジュールバージョンアップグレード

#### バグ修正
- レプリケーショングループ作成時に、インターネットゲートウェイを設定をしないユーザーのVPCサブネットを選択した場合、失敗する現象を修正

### 2020. 01. 21.

#### 機能改善

- コンソール画面とイベントのメッセージ日本語対応
- Failover後、ドメイン変更失敗の際イベント登録追加

### 2019. 12. 24.

#### 新規サービスリリース

- TOAST EasyCacheは、Redis(REmote DIctionary Server)をクラウド環境で提供するサービスです。
- 簡単な設定で高可用性(自動HA)のRedisサーバーを使用できます。
- Redis 3.2.12バージョンを提供します。
