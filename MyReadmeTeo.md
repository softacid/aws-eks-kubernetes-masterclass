setup cluster:

eksctl create cluster --name=eksdemo1 \
                      --region=eu-west-1 \
                      --zones=eu-west-1a,eu-west-1b \
                      --without-nodegroup



OIDC
eksctl utils associate-iam-oidc-provider \
    --region eu-west-1 \
    --cluster eksdemo1 \
    --approve


NodeGroups

eksctl create nodegroup --cluster=eksdemo1 \
                        --region=eu-west-1 \
                        --name=eksdemo1-ng-public1 \
                        --node-type=t3.medium \
                        --nodes=2 \
                        --nodes-min=2 \
                        --nodes-max=4 \
                        --node-volume-size=20 \
                        --ssh-access \
                        --ssh-public-key=kube-demo \
                        --managed \
                        --asg-access \
                        --external-dns-access \
                        --full-ecr-access \
                        --appmesh-access \
                        --alb-ingress-access
