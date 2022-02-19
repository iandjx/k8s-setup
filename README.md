1. Setup kubectl

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectlchmod +x ./kubectlsudo mv ./kubectl /usr/local/bin/kubectl
```

2. Setup AWS cli

```
pip install awscli --upgrade --user
```

3. Create IAM user

   1. Create IAM user with Admin access
   2. Create policy and attach to IAM user
      - eks-policy
      - cloud-formation-policy
      - AmazonEC2FullAccess
      - IAMFullAccess
      - AmazonVPCFullAccess

4. Install Helm

   ```
   curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

   chmod 700 get_helm.sh

   ./get_helm.sh

   helm version
   ```

5. Deploy ingress

   ```
   helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

   helm install ingress-nginx ingress-nginx/ingress-nginx
   ```

6. Create route 53 hosted zone

   - Record type: A
   - Route traffic: Alias to Ingress load balancer
   - Routing policy: Simple routing

7. Deploy cert manager

   ```
   helm repo add jetstack https://charts.jetstack.io

   helm install cert-manager --namespace cert-manager --create-namespace jetstack/cert-manager --version v1.5.3 --set installCRDs=true

   kubectl apply -f issuer.yml

   kubectl get clusterissuer
   ```

8. https://faun.pub/eks-with-nginx-ingress-controller-and-helm3-daee18175d45

https://medium.com/cloud-prodigy/configure-letsencrypt-and-cert-manager-with-kubernetes-3156981960d9
