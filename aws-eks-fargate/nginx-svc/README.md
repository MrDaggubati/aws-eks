10. deploy the ingress object

```sh
$ kubectl apply -f nginx-ingress.yml
```

11. lookup the alb-ingress-controller pod name and watch its logs

```sh
# lookup the pod id
$ kubectl get po -A  | grep alb-ingress
# logs -f to watch the pod logs. Make sure you specify correct pod name
$ kubectl -n kube-system logs -f po/alb-ingress-controller-78cb78cffb-ddkj8

$ kubectl logs -f $(kubectl get po -n kube-system | egrep -o 'alb-ingress-controller-[A-Za-z0-9-]+') -n kube-system

```

*some handy commands to check pods and manifests*
 ```sh
$ kubectl get pods -n kube-system
$ kubectl get deploy -n kube-system
$ kubectl logs -f $(kubectl get po -n kube-system | egrep -o 'alb-ingress-controller-[A-Za-z0-9-]+') -n kube-system
```

12. Now describe the ingress object to find out the **ALB DNS name** and curl the ALB

 kubectl describe ingress/nginx-ingress

![](images/eks-fargate-07.png)

You will see the welcome message from nginx.


```sh
kubectl delete -f nginx-deploy-svc.yaml
kubectl delete -f nginx-ingress.yaml
kubectl delete -f alb-ingress-controller.yaml
eksctl --region ap-northeast-1 delete cluster --name eks-fargate-cluster
```

