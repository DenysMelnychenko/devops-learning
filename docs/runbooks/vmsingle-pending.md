# VMSingle pod застряг у Pending

## Симптоми
- `kubectl get pods -n monitoring` показує vmsingle у статусі Pending
- `kubectl get pvc -n monitoring` показує PVC у статусі Pending

## Причина
k0s не має вбудованого StorageClass провізіонера.
PVC не може знайти де виділити диск.

## Рішення
1. Встановити local-path-provisioner:
   kubectl apply -f k8s/storage/local-path-provisioner.yaml

2. Зробити його дефолтним:
   kubectl patch storageclass local-path \
     -p '{"metadata":{"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'

3. Видалити застряглий PVC і перезапустити оператор:
   kubectl delete pvc -n monitoring <ім'я PVC>
   kubectl rollout restart deployment -n monitoring vm-stack-victoria-metrics-operator
