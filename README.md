# DevFest Modena 2024

Codice della presentazione [Dal Caos al Controllo: Il Viaggio nell'Infrastructure as Code, da Docker Compose a Kubernetes](https://devfest.modena.it/speaker/giovanni-perteghella)

## Esecuzione locale 

```
docker compose up
```

## Esecuzione immagine dal repository 

```
docker compose -f docker-compose-image1.0.yaml up
```

Proviamo la v2.0
```
docker compose -f docker-compose-image1.0.yaml up
```


## Esecuzione immagine con 2 istanze 

Proviamo a scalare la nostra app a 2 istanze, necessitiamo di un load balancer, ad esempio nginx e la relativa configurazione

```
docker compose -f docker-compose-image1.0-multi.yaml up
```

Questa funziona in locale, per metterla online abbiamo comunque bisogno di fare il build di nginx

## Build immagine 

```
docker buildx build --platform linux/amd64,linux/arm64 --tag perteghella/devfest-modena-2024:1.0 --push .
```

## Kubernetes

Colleghiamoci al cluster

```
kubectl get nodes
```

Eseguiamo i manifest di redis

```
kubectl apply -f redis.yaml
```

Verifichiamo

```
kubectl get pods
kubectl get deployment
kubectl get service
```

Eseguiamo i manifest dell'applicazione

```
kubectl apply -f web.yaml
```

Verifichiamo

```
kubectl get pods
kubectl get deployment
kubectl get service
```

Eseguiamo i manifest per esporre dell'applicazione su internet

```
kubectl apply -f ingress.yaml
```

Verifichiamo la raggiungibilità della nostra applicazione 

```
http://hello-world.41c5d02c-fa48-483a-b52f-6bdfc0a771b1.k8s.civo.com/
```