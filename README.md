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
  ubuntu-test: #サービス名はdevcontainer.jsonのサービス名と合わせる。
    image: ubuntu
    tty: true # これをしないとコンテナが起動し続けないのでエラーになる。
    working_dir: /work # これをしないとworkフォルダができないのでエラーになる。
    volumes: 
      - ../work:/work # ホストとのボリューム共有。../workは上のフォルダ構造で示した※1の一つ上の階層のworkフォルダを指し示す。
```

`devcontainer.json`

```json
{
  "name": "ubuntu-devcontainer-project",
  "dockerComposeFile": [
      "./docker-compose.yml"
  ],
  "service": "ubuntu-test",
  "workspaceFolder": "/work"
} 
```

