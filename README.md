# Simple VSCode Remote Container

シンプルなVSCode Remote Containerのファイル構成

```bash
/
　├ .devcontainer/
  │ ├ devcontainer.json
  │ └  docker-compose.yml
　└ work/ ※1
```

`docker-compsoer.yml`

```yml
version: '3.3'

services:
  centos-test: #サービス名はdevcontainer.jsonのサービス名と合わせる。
    image: centos:centos7
    tty: true # これをしないとコンテナが起動し続けないのでエラーになる。
    working_dir: /work # これをしないとworkフォルダがないのでエラーになる。
    volumes: 
      - ../work:/work  # ホストとのボリューム共有。../workは上のフォルダ構造で示した※1の一つ上の階層のworkフォルダを指し示す。
    privileged: true
    command: /sbin/init # privileged true，sbin/initをしないとsystemctlが権限の問題で動かない。
```

`devcontainer.json`

```json
{
  "name": "centos-devcontainer-project",
  "dockerComposeFile": [
      "./docker-compose.yml"
  ],
  "service": "centos-test",
  "workspaceFolder": "/work"
} 
```

