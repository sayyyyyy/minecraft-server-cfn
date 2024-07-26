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
