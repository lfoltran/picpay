# Instalando docker

Para instalar o docker, utilizar a sequencia de comandos. (Base em ubuntu x64)

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt update
# Grantir que está apontando para o pacote correto
apt-cache policy docker-ce

docker-ce:
  Installed: (none)
  Candidate: 5:20.10.13~3-0~ubuntu-focal
  Version table:
     5:20.10.13~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.12~3-0~ubuntu-focal 500

apt-install docker-ce

#Resultado após instalação
systemctl status docker

Esperado:
docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2022-03-13 13:12:35 -03; 9s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 467655 (dockerd)
      Tasks: 12
     Memory: 27.8M
     CGroup: /system.slice/docker.service
             └─467655 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```

# Instalando o configMap
kubectl apply -f ./k8s/simpleapp-cm.yaml

# Instalando a aplicação
kubectl apply -f ./k8s/simpleapp.yaml

# Instalando Grafana e Prometheus
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/kube-prometheus-stack
```

A vantagem da utilização da stack é a agilidade de instalação e garantia de um monitoramento funcionando bastante rápido.

# Acessando Grafana
```
kubectl port-forward deployment/prometheus-grafana 3000
```

Acessar browser em http://localhost:3000

user: admin
pass: prom-operator

![Screenshot from 2022-03-13 13-34-05](https://user-images.githubusercontent.com/88778728/158069887-fd3fab07-0505-4b8a-81bc-65b54d66984c.png)
