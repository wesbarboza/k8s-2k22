# Kubernetes
## Comandos básicos
**Pre-req**
```
echo "source <(kubectl completion bash)">> /root/.bashrc
kubectl config get-contexts
```

**Utilizando get**
```
kubectl get all
kubectl get nodes
kubectl get pods --all-namespaces
// namespace especifico: -n namespace
// mais detalhes: -o wide
```
**Utilizando describe**
```
kubectl describe
```
**explain service, pods, etc**
```
kubectl explain xxx
```

**criar namespace**
``` 
kubectl create namespace nome_namespace
```

**criar pod com run**
```
kubectl run nginx --image=nginx 
kubectl run nginx --image=nginx  --dry-run=client
```
**visualizar pod especifico**
```
kubectl get pods nginx -o wide
// get all
// get pods,nodes, etc...
```

**exportar yaml do pod**
```
kubectl get pods nginx -o yaml
```
**criando a partir de arquivo**
```
kubectl create -f nome_arquivo.yaml
```

**delete**
```
kubectl delete -f nome_arquivo.yaml
kubectl delete pods nginx //apagar pod específico.
// pods, services, namespaces, etc.
```

**criar um template yml**
```
kubectl run nginx --image=nginx  --dry-run=client -o yaml > nome_arquivo.yml
```

**irá exibir uma saida:**
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

**Criando pod a partir do arquivo yaml**
```
kubectl create -f nome_do_arquivo.yaml
```

**Criar um service para um pod, deployment, etc. usando expose**
```
kubectl expose pod nginx //irá criar type default = ClusteIP
// Para criar com tipo NodePort para ser acessível externamente
kubectl expose pod nginx --type=NodePort

```

```kubectl get service
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.43.0.1      <none>        443/TCP   137m
nginx        ClusterIP   10.43.140.40   <none>        80/TCP    20s
```

**describe**

```
kubectl describe services nginx
Name:              nginx
Namespace:         default
Labels:            run=nginx
Annotations:       <none>
Selector:          run=nginx
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.43.140.40
IPs:               10.43.140.40
Port:              <unset>  80/TCP
TargetPort:        80/TCP
Endpoints:         10.42.0.18:80
Session Affinity:  None
Events:            <none>
```

**Editando um service**
```
kubectl edit service nginx
```

**criando deployment**
Utilizando modelo de arquivo
```
kubectl apply -f deployment.yaml
```
Criando service para o deployment
```
kubectl expose deployment nginx-deployment --type=NodePort
```
