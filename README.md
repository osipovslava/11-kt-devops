# Развертывание Minikube и работа с манифестами

## Описание задания

Это практическое задание направлено на освоение основ работы с Kubernetes, в частности, на развертывание Minikube и работу с манифестами. В процессе выполнения задания вы настроите Minikube, создадите и исправите Pod манифесты, а также выполните основные команды kubectl.

## Шаги выполнения задания

### Шаг 1: Развертывание Minikube

1. Установите Minikube на ваш рабочий компьютер или виртуальную машину, следуя официальной [документации по установке Minikube](https://minikube.sigs.k8s.io/docs/start/).
2. Запустите Minikube с помощью команды:
   ```bash
   minikube start
   ```

### Шаг 2: Создание Pod манифеста

1. Создайте файл `pod.yaml` и скопируйте в него следующий манифест:
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: my-nginx
   spec:
     containers:
     - name: nginx-container
       image: nginx:1.10
   ```
2. Попробуйте создать Pod из этого манифеста с помощью команды:
   ```bash
   kubectl create -f pod.yaml
   ```
3. Если команда завершится ошибкой, убедитесь, что структура файла корректна. В данном случае, ошибка вызвана неправильной вложенностью. Исправьте файл следующим образом:
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: my-nginx
   spec:
     containers:
     - name: nginx-container
       image: nginx:1.10
   ```

### Шаг 3: Запуск Pod Redis

1. Запустите Pod Redis в кластере с помощью команды:
   ```bash
   kubectl run redis --image=redis:5.0 -n default
   ```
2. Проверьте, что Redis запущен и находится в статусе `Running`, с помощью команды:
   ```bash
   kubectl get pods -n default
   ```
3. Удостоверьтесь, что версия Docker image — `redis:5.0`, с помощью команды:
   ```bash
   kubectl get pod redis -n default -o jsonpath="{..image}"
   ```
4. Отредактируйте Pod Redis для изменения версии Docker image на `redis:6.0`:
   ```bash
   kubectl edit pod redis -n default
   ```
   Для изменения текстового редактора по умолчанию, используйте переменную окружения `KUBE_EDITOR`, например:
   ```bash
   export KUBE_EDITOR=nano
   ```
5. Сохраните изменения и проверьте логи контейнера с помощью команды:
   ```bash
   kubectl logs redis -n default
   ```
