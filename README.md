# OPA Gatekeeper Policy Rules

## Concepts
+ https://www.openpolicyagent.org/docs/latest/
+ https://kubernetes.io/blog/2019/08/06/opa-gatekeeper-policy-and-governance-for-kubernetes/


## Videos
+ https://www.youtube.com/watch?v=xrGHSdhYh4Y&t=139s
+ https://www.youtube.com/watch?v=urvSPmlU69k&t=19s

## Install opa getekeeper
``
sh install.sh
``

## Requirements
 + minikube
 + opa gatekeeper 
 + Rego basic understanding

## Rules

+ k8s_image_validation
+ k8s_mandatory_labels

### TODO
+ Disbale previliged containers
+ Allow specific users in specific namespaces
+ Allow securitycontext like fsgroup , RunAsUser
+ Allow 420 mode only to mount volumes
+ Labels should not be duplicated 
+ Microservice based required lables


### Input Document reference to write template

https://www.openpolicyagent.org/docs/latest/kubernetes-primer/#input-document

```
{
    "kind": "AdmissionReview",
    "request": {
        "kind": {
            "kind": "Pod",
            "version": "v1"
        },
        "object": {
            "metadata": {
                "name": "myapp",
                "labels": {
                    "costcenter": "fakecode"
                }
            },
            "spec": {
                "containers": [
                    {
                        "image": "nginx",
                        "name": "nginx-frontend"
                    },
                    {
                        "image": "mysql",
                        "name": "mysql-backend"
                    }
                ]
            }
        }
    }
}

```
The request object structure in Admission Review is same as the K8s Object request in JSON format and it accept same dot notations. 

For testing and verification use Rego playgroud (https://play.openpolicyagent.org/)




