# school-dev-k8s

Все работы проводим на sbox.slurm.io:
ssh sbox.slurm.io

Форк проекта

Открываем в браузере репозиторий xpaste. Он находится по адресу

https://gitlab.com/slurm-io/xpaste

Справа на одной линии с названием проекта видим кнопку fork. Нажимаем ее.
Выбираем в качестве нэймспэйса в следующем окне свой логин.
И дожидаемся окончания процесса форка.
Последним шагом клонируем получившийся форк к себе на админбокс.

cd ~
git clone https://gitlab.com/<наименование своего нэймспэйса>/xpaste.git

команды
k = kubectl
po = pod
rs = replicaset
deploy = deployments
deployment = deployments
deployments = deployments
можно добавить в deployments через точку апиверсион пример deployments.apps

k completion -h - инструкция как добавить комплишин

k get node - получить список нод
k get pod - получить список подов
k get po -A - получить список подов по всем неймспейсам
k get replicaset - получить реплики сет
k get po -l app=my-app - выведет поды с таким labels
k get deployments - получить список деплойментов

k create -f pod.yaml - создать под из файла, применяется только 1 раз
k apply -f pod.yaml - создает под, если под уже существует применяет изменения в файле

k describe pod my-pod - выведет информацию про под
k describe po - выведет информацию по всем подам

k delete pod my-pod - удаление пода по имени
k delete -f pod.yaml - удаление подов из файла

k scale --replicas 3 replicaset my-replicaset - устанавливает количество реплик для заданного реплика сет

k set image replicaset my-replicaset nginx=nginx:stable-alpine3.20-perl - меняем образ контейнера в репликасете(в темплейте)(в данном случае контейнера nginx) но не меняет в поде самостоятельно
k set image replicaset my-replicaset '*=nginx:stable-alpine3.20-perl' - меняет образ всех контейнеров в репликасете(в темплейте) но не меняет в поде самостоятельно
k set image deployments my-deployment '*=nginx:stable-alpine3.20-perl' - меняет образ всех контейнеров в деплойменте(в темплейте) и в подах

k explain - показать документацию в консоли
примеры:
 - k explain pod
 - k explain pod.spec 
 - k explain pod.spec.containers

k edit deploy my-deployment - редактирование объекта на лету

k rollout history deploy my-deployment - история ревизий
k rollout undo deploy my-deployment - роллбэк деплоимента(реплик в нем)

Меняем количество ресурсов для нашего деплоймента
 - kubectl patch deployment my-deployment --patch '{"spec":{"template":{"spec":{"containers":[{"name":"nginx","resources":{"requests":{"cpu":"10"},"limits":{"cpu":"10"}}}]}}}}'
