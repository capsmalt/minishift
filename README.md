# macOS で minishift 

## Homebrew 導入
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
$ brew install wget
```

## minishift 導入
```
$ brew cask install minishift
$ minishift version
```

## mac用の仮想化ドライバー導入
```
$ brew install docker-machine-driver-xhyve
$ sudo chown root:wheel /usr/local/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
$ sudo chmod u+s /usr/local/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
$ git -C "$(brew --repo homebrew/core)" fetch --unshallow
```

## minishift 起動
```
$ minishift start --vm-driver xhyve
```

## oc コマンドのパスを通す
```
$ eval $(minishift oc-env)

# .bash_profileなどに記載する場合
$ export PATH="$HOME/.minishift/cache/oc/v3.10.0/darwin:$PATH"
```


## アプリをお試し作成
```
$ oc new-app https://github.com/sclorg/nodejs-ex -l name=myapp
$ oc logs -f bc/nodejs-ex
$ oc expose svc/nodejs-ex
```

## Kubernetesリソースの動作確認
```
$ oc get pods
$ oc get svc
$ oc get deploy
$ oc get all
```

## ブラウザで動作確認
`$ minishift openshift service nodejs-ex --in-browser`

## minishift 停止
`$ minishift stop`
