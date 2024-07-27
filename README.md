# minecraft-server-cfn
## 概要
Minecraftマルチサーバーを作成するCloudFormationテンプレート群

## 作成するリソース
### Minecraft-Server-Base
- VPC
- InternetGateway
- Subnet
- RouteTable
- SecurityGroup
- IAM Role

### Minecraft-Server-EC2
- EC2 Instance

### Minecraft-Server-Scheduler
- IAM Role
- EventBridge Scheduler

## 利用方法
1. [こちら](https://mcversions.net/)のサイトで遊びたいバージョンのサーバーのダウンロードリンクを取得する
    - バージョンを選択し、Download Server jarを右クリックしてリンクをコピーする
2. AWSにサインインする
3. リージョンを自分の住んでいる地域の近くにする
4. CloudFormationの画面を開く
5. CloudFormationテンプレートを流してスタックを作成する
    1. スタックの作成＞新しいリソースを使用（標準）を押下
    2. テンプレートのアップロード＞ファイルの選択を押下し、以下のCloudFormationテンプレートをアップロード
        1. `Minecraft-Server-Base.yml`
            - Parameters
                - なし
        2. `Minecraft-Server-EC2.yml`
            - Parameters
                - MinecraftServerUrl: 手順1で取得したダウンロードリンク
                - JavaVersion: Minecraftのバージョンに合わせたJavaバージョン
                    - ~1.16: Java11
                    - 1.17~: Java16
                    - 1.18~: Java17
                    - 1.20.5~: Java21
                - MemorySize: 大人数でなければデフォルト
    3. スタックオプションはデフォルトで次に進む
    4. `AWS CloudFormation によって IAM リソースが作成される場合があることを承認します。`にチェックを入れて送信ボタンを押下
    - 注意点
        - IAMを変更するため確認画面でチェックをつける必要がある
        - スタックを作成する順番を逆にするとうまくいかないため注意
        - インスタンス起動のタイミングで[EULA](https://www.minecraft.net/ja-jp/terms/r3)に自動的に同意するため注意
6. EC2の画面を開き、パブリックIPv4アドレスをコピーする
7. MinecraftでサーバーIPの欄にパブリックIPv4アドレスをつけてサーバーに接続する
    - EC2インスタンスが作成された後もインスタンス内部で設定を行っているため10分程待ってからアクセスする必要がある
8. 遊び終わったらEC2インスタンスを停止する
    - 稼働させている限り料金が発生してしまう
    - 停止ではなく終了してしまうとデータが消えてしまうので、理由がない限り停止を推奨