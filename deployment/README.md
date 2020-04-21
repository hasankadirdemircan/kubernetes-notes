#get all
kubectl get all

#delete replicaset
kubectl delete rs webapp

#deployment update
kubectl apply -f pod.yaml

#rollout status
kubectl rollout status webapp

#rolluot
kubectl rollout status deploy webapp
(deploy->deployment)

#history
kubectl rollout history deploy webapp


#rollout
kubectl rollout undo deploy webapp
