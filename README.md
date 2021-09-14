# vscode-env-remote-esp-idf

ESP-IDFのコンパイル環境です。  
https://hub.docker.com/r/espressif/idf/

# 事前準備

次のツールをインストールします。

- [git](https://git-scm.com/)
- [Docker](https://www.docker.com/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Visual Studio Code Remote - Containers](https://code.visualstudio.com/docs/remote/containers)


# 使い方

1. 本リポジトリを取得します。 - `git clone https://github.com/jp-rad/vscode-env-remote-esp-idf.git`
1. Visual Studio Codeで開きます。
1. `Reopen in Container`を実行します。
1. `ws`フォルダ内でコーディングします。
1. ESP-IDF(`make`コマンドや`idf.py`ツール)でコンパイルします。


# 例：ESP32版 micropython のビルド

本リポジトリを取得します。
```
cd yourworkfolder
git clone https://github.com/jp-rad/vscode-env-remote-esp-idf.git
```

[micropython](https://github.com/micropython/micropython.git)のリポジトリを取得します。
```
cd vscode-env-remote-esp-idf/ws
git clone https://github.com/micropython/micropython.git
```

取得した本リポジトリのフォルダをVisual Studio Codeで開きます。
```
cd yourworkfolder
code vscode-env-remote-esp-idf
```

`.devcontainer/devcontainer.json`ファイルを開き、`workspaceFolder`で、`micropython`のフォルダを指定します(コメントアウトを解除します)。
```
	//"workspaceFolder": "/home/vscode/ws",
	"workspaceFolder": "/home/vscode/ws/micropython",
```

左下の`Open a Remote Window`アイコンをクリックし、画面上部のドロップダウンリストから`Reopen in Container`を選択してDockerコンテナを起動します。  
*※初回の起動は、イメージファイル等をダウンロードするため、数分かかります。*

新しいターミナルを開き(`bash`)、次の手順でビルドします。
```
cd /home/vscode/ws/projects/micropython
make -C mpy-cross
cd ports/esp32
make submodules
make
```

`build-GENERIC`フォルダに作成された`firmware.bin`ファイルがESP32用のmicropythonファームウェアですので、`esptool.py`等でESP32へ転送してください。
