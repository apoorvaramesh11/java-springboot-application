
# to make application secure we use this ingress
~~~

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: springboot-ingress
  annotations:
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/target-type: ip
    alb.ingress.kubernetes.io/listen-ports: '[{"HTTP":80},{"HTTPS":443}]'
    alb.ingress.kubernetes.io/certificate-arn: arn:aws:acm:ap-south-1:289835835122:certificate/7563b8c1-786a-413e-a4cd-7a149963983b
spec:
  ingressClassName: alb
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: springboot-svc
            port:
              number: 8080

~~~



# to fetch argocd UI password
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
