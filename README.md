## 1. Network Policies: Permitir tráfico dentro del mismo Namespace

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-same-namespace
  namespace: game-2048
spec:
  podSelector:
    matchLabels:
      app.kubernetes.io/name: app-2048
  ingress:
    - from:
        - podSelector: {}
  policyTypes:
    - Ingress
```

Este NetworkPolicy, llamado "allow-same-namespace", está diseñado para los pods en el namespace "game-2048" que tienen la etiqueta "app.kubernetes.io/name: app-2048". Permite que cualquier otro pod dentro del mismo namespace "game-2048" se comunique con ellos.

## 2. Inbound Network Policies: Permitir tráfico desde Pods con una etiqueta específica

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-from-specific-label
  namespace: game-2048
spec:
  podSelector:
    matchLabels:
      app.kubernetes.io/name: app-2048
  ingress:
    - from:
        - podSelector:
            matchLabels:
              access: granted
  policyTypes:
    - Ingress
```

Esta política, llamada "allow-from-specific-label", está configurada para los pods que tienen la etiqueta "app.kubernetes.io/name: app-2048" en el namespace "game-2048". Solo permite el tráfico entrante de otros pods que tienen la etiqueta "access: granted".

## 3. External Network Policies: Permitir tráfico desde una dirección IP específica

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-from-specific-ip
  namespace: game-2048
spec:
  podSelector:
    matchLabels:
      app.kubernetes.io/name: app-2048
  ingress:
    - from:
        - ipBlock:
            cidr: 203.0.113.0/24
  policyTypes:
    - Ingress
```

El NetworkPolicy "allow-from-specific-ip" se aplica a los pods etiquetados con "app.kubernetes.io/name: app-2048" en el namespace "game-2048". Esta política permite el tráfico entrante solo desde la dirección IP o rango especificado, en este caso, "203.0.113.0/24".

