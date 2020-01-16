Для установки minikube
 устанавливаем choco, после выполняем 
 ``` 
choco install minikube
kubectl	config	view
```
копипастим вывод в файлик и его можно использовать для подключения к кластеру
но большинство сред разработки уже умеют цеплять minikube
например, ставим плагин в visual studio code и жамкаем "add cluster"

Краткая информация по k8s

```
kubectl cluster-info
```

Советую установить дашборд для визуализации
https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

для этого выполните

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta1/aio/deploy/recommended.yaml

и примените файлики из ./connect-to-dashboard
 
 Далее запустите 

 ```
 kubectl proxy
 ```

 эту консоль не закрывать, а откройте новую и выполните 
 ```
 kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')

```
команда работает и на win, если использовать bash-for-git

там найдете token, его нужно вставить при логине в дашборд

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

Теперь, если вы 

попробуете зайти по ssh на машинку и удалить все контейнеры, увидите, что все останется живо
```
minikube ssh
docker ps
docker rm -f $(docker ps -a -q)
```

Это связано с тем, что у каждого контейнера есть контроллер реплик в виде деплойментов, демонсетов, и т д. Именно они и следят за состоянием подов

Эти поды тоже можно убить
```
kubectl get pods -n kube-system
kubectl delete pod --all -n kube-system
```

Проверить, что миникуб живой
```
kubectl get cs
```

Как восстанавливается kube-dns?
Используемый в нём addon manager периодически проверяет (и поддерживает) состояние конфигураций всех установленных дополнений, одним из которых является kube-dns. В кубере как deployment в kube-system

Как восстанавливается kube-apiserver?
За ним следит Deployment, он же и поднимает реплики


______

Создать Pod

```
kubectl apply -f web-pod.yaml
```

Пробросить порты

```
kubectl port-forward  pod/web 8000:8000
```

```
kubectl describe pod web
```

Под содержит пример init-container c общим volume







