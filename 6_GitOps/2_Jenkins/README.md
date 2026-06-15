# Задача

**Завдання створити Jenkins Pipeline для мульти-платформенної параметризованої збірки для свого репозиторію GitHub.**

В якості агента використати хост/контейнер, на якому розгорнуто Jenkins.

Для виконання рекомендується декларативний формат Jenkins Pipeline: https://www.jenkins.io/doc/book/pipeline/

**Приклад виконання:**

1. Встановіть Kind та Kubernetes на ваш локальний комп'ютер.
2. Створіть кластер Kubernetes за допомогою Kind:
```bash
kind create cluster --name jenkins
```
      
3. Встановіть Jenkins на кластер Kubernetes за допомогою Helm:
```bash
helm repo add jenkinsci https://charts.jenkins.io/
helm repo update
helm install jenkins jenkinsci/jenkins
```
      
4. Після запуску Jenkins отримайте доступ до інтерфейсу користувача Jenkins за допомогою наступної команди:
```bash
kubectl port-forward svc/jenkins 8080:8080
```
      
5. Тепер ви можете отримати доступ до Jenkins за адресою у вашому веббраузері:
```bash
http://localhost:8080
```
      
## **Завдання:**

1. Візьміть за основу Jenkins Groovy приклад:
[https://github.com/den-vasyliev/kbot/blob/main/pipeline/jenkins.groovy](https://https://github.com/den-vasyliev/kbot/blob/main/pipeline/jenkins.groovy)
  
2. Налаштуйте Jenkins Pipeline для створення параметризованої збірки за використанням pipeline скрипту з вашого репозиторію як зображено на прикладі:
[https://github.com/den-vasyliev/kbot/blob/main/pipeline/jenkins-pipeline.png](https://https://github.com/den-vasyliev/kbot/blob/main/pipeline/jenkins-pipeline.png)
  
3. Розробник повинен мати можливість вибрати параметри збірки або використати налаштування по замовчуванню, наприклад:
https://github.com/den-vasyliev/kbot/blob/main/pipeline/jenkins-job.png
  
Відповідь: посилання на RAW файл pipeline/jenkins.groovy у вашому репозиторії.