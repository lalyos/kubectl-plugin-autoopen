This kubect plugin will autoopen NodePort services in your default browser.

## Installation


Installing this plugin is easy:
```
mkdir -p ~/.kube/plugins/
git clone https://github.com/lalyos/kubectl-plugin-zed.git ~/.kube/plugins/zed
```

To validate that the plugin installation was succesfull run the plugin command:
```
$ kubectl plugin
Runs a command-line plugin. 

Available Commands:
  autoopen    svc autoopen
```

## Usage

Run the autoopen plugin in a separate terminal:
```
kubectl plugin autoopen
```

From now on, all new NodePort type services will be opened in the browser.
To test it with a plain old nginx svc:
```
kubectl run delme \
  --image=nginx \
  --port=80 \
  --expose \
  --service-overrides='{"spec":{"type":"NodePort"}}'
```

To delete the test service:
```
kubectl delete deployment,svc delme
```

## Configuration

A small delay is needed to check that the newly created service is reachable.
A sleep delayed curl is used to chec availabilty. By default it waits for **3 scends**.
For slower services you can change it with the `SLEEP` env variable:

```
SLEEP=5 kubectl plugin  autoopen
```

## Debug

If you want to see the whats happening uner the hood, use the `--debug` option:
```
kubectl plugin  autoopen --debug=true
```


