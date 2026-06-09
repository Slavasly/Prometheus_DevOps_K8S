Ви отримали листа від рекрутинг-менеджера проєкту, який вимагає досвіду сучасних DevOps рішень по автоматизації інфраструктури. Вас запросили підготовувати та надіслати маркетингове резюме, що включає розділ реалізованих інженерних рішень.

Hello,

I hope this email finds you well. I came across your profile and I wanted to reach out to you regarding a potential contractor opportunity for a project that we are currently working on.

The project is focused on marketing automation and we are looking for a skilled and experienced professional to assist us with prompt engineering solutions. We believe that your expertise and experience would be a great fit for our team.

To move forward with this opportunity, we kindly ask that you prepare a marketing resume that highlights your most relevant experience and skills. In addition, we would like you to provide us with examples of prompt engineering solutions that you have implemented in the past, and how they contributed to the success of the project.

Please note that for this, all we require is a GitHub repository containing your YAML Kubernetes manifests with prompt. You do not need to provide a Docker image or deploy the application to a Kubernetes cluster. We will review your YAML manifests and provide feedback accordingly.

If you are interested in pursuing this opportunity, please let us know and we will provide you with more details about the project and the next steps in the selection process.

We are looking forward to hearing from you soon and we hope that we can have the opportunity to work together.

Best regards!
    
Зверніть увагу, що для виконання цього завдання потрібне лише посилання на GitHub-репозиторій з YAML-маніфестами Kubernetes та prompts для їх генерування. Вам не потрібно надавати образи Docker чи розгортати додаток на кластері Kubernetes.

Виконайте наступні кроки:

Створіть портфоліо власних промптів (prompt) англійською мовою для генерації та аналізу Kubernetes-маніфестів зі списку: (https://github.com/den-vasyliev/go-demo-app/tree/master/yaml):
app.yaml
app-livenessProbe.yaml
app-readinessProbe.yaml
app-volumeMounts.yaml
app-cronjob.yaml
app-job.yaml
app-multicontainer.yaml
app-resources.yaml
app-secret-env.yaml
2. Ознайомтесь із принципами Prompt Engineering за допомогою документа: Prompt Engineering від Googlehttps://www.kaggle.com/whitepaper-prompt-engineering

3. Скористайтесь AI-інструментом від Google Cloud для роботи з Kubernetes: https://github.com/GoogleCloudPlatform/kubectl-ai

Формат відповіді: посилання на репозиторій, де Readme файл містить таблицю у форматі NAME:PROMPT:DESCRIPTION:EXAMPLE, де EXAMPLE — це посилання на результуючий маніфест у директорії yaml в корні репозиторію.

Додаткове завдання (опціональне, не оцінюється)

Перехід на Gateway API

Ти щойно створив свої перші ресурси.  Один з таких ресурсів може бути Ingress. Це ресурс для управління доступом і маршрутизації зовнішнього трафіку до сервісів у кластері Kubernetes. Але в 2025 році індустрія переходить на Gateway API - новий стандарт Kubernetes для HTTP-роутингу.

Завдання:

Встанови ingress2gateway CLI-інструмент для автоматичної конвертації:

`

bashgo install sigs.k8s.io/ingress2gateway@latest

`

Конвертуй свій Ingress маніфест:

`

bashingress2gateway print --input-file ingress.yaml

`

Переглянь що згенерували два ресурси: Gateway і HTTPRoute. Порівняй із оригінальним Ingress.

Яка ключова різниця між Ingress і HTTPRoute?
Хто має керувати Gateway, а хто HTTPRoute і чому?

📎 Ресурси:

https://gateway-api.sigs.k8s.io/
https://gateway-api.sigs.k8s.io/guides/getting-started/migrating-from-ingress-nginx/

# Встановіть та налаштуйте kubectl-ai плагін для створення ШІ Recommended YAML manifests

## Task steps
1. Create an [API key](https://platform.openai.com/account/api-keys)  
`key name: name: kubectl-ai`  

2. Install and configure [the kubectl-ai plugin](https://github.com/sozercan/kubectl-ai)
```sh
$ wget https://github.com/sozercan/kubectl-ai/releases/download/v0.0.11/kubectl-ai_linux_amd64.tar.gz
$ tar -zxvf kubectl-ai_linux_amd64.tar.gz
$ mv kubectl-ai /usr/local/bin/
$ chmod +x /usr/local/bin/kubectl-ai

$ kubectl plugin list                                                                                
The following compatible plugins are available:
/root/.krew/bin/kubectl-krew
/root/.krew/bin/kubectl-ns
/usr/local/bin/kubectl-ai
/usr/local/bin/kubectl-kubeplugin

$ nano ~/.zshrc
export OPENAI_API_KEY="***************************"

$ source ~/.zshrc

$ export OPENAI_DEPLOYMENT_NAME="gpt-4"
```

3. Practice writing and testing prompts on a local cluster
```yaml
$ k ai "get status of master node" --require-confirmation=false
✨ Attempting to apply the following manifest:

apiVersion: v1
kind: Pod
metadata:
  name: node-status-check
  namespace: default
spec:
  containers:
  - name: check-node-status
    image: bitnami/kubectl:latest
    command: ['/bin/bash', '-c', 'kubectl get node master -o jsonpath="{.status}"'] 
    resources:
      requests:
        cpu: 100m
        memory: 100Mi
  restartPolicy: OnFailure

$ mkdir yaml
$ kubectl ai "create an nginx deployment with 3 replicas" --require-confirmation=false > yaml/app.yaml
```

4. The resulting manifest in the yaml directory in the root of the repository.

| NAME                        | PROMPT                             | DESCRIPTION                                                              | EXAMPLE                                     |
|-----------------------------|------------------------------------|--------------------------------------------------------------------------|---------------------------------------------|
| app.yaml                    | Create Application Config          | YAML to define the basic schema of a Kubernetes application              | [app.yaml](yaml/app.yaml)                 |
| app-livenessProbe.yaml      | Add Liveness Probe                 | YAML to define a liveness probe for your application                    | [app-livenessProbe.yaml](yaml/app-livenessProbe.yaml) |
| app-readinessProbe.yaml     | Add Readiness Probe                | YAML to define a readiness probe for your application                   | [app-readinessProbe.yaml](yaml/app-readinessProbe.yaml) |
| app-volumeMounts.yaml       | Configure Volume Mounts            | YAML to define and configure storage volumes for your application       | [app-volumeMounts.yaml](yaml/app-volumeMounts.yaml) |
| app-cronjob.yaml            | Create Cron Job                    | YAML to define a cron job within your application                       | [app-cronjob.yaml](yaml/app-cronjob.yaml) |
| app-job.yaml                | Create a Job                       | YAML to define a job within your application                            | [app-job.yaml](yaml/app-job.yaml) |
| app-multicontainer.yaml     | Set Up Multi-container Pods        | YAML to define a pod that runs more than one container                  | [app-multicontainer.yaml](yaml/app-multicontainer.yaml) |
| app-resources.yaml          | Configure Resource Usage           | YAML to configure resource requests and limits for your application     | [app-resources.yaml](yaml/app-resources.yaml) |
| app-secret-env.yaml         | Set Up Secrets as Env Variables    | YAML to define environment variables using secrets                      | [app-secret-env.yaml](yaml/app-secret-env.yaml) |

                                                                            
   NAME            │ PROMPT           │ DESCRIPTION      │ EXAMPLE            
  ─────────────────┼──────────────────┼──────────────────┼──────────────────  
   app-            │ Generate         │ Defines a        │  apiVersion: bat   
   cronjob.yaml    │ manifest         │ CronJob for      │ ch/v1 kind: Cron   
                   │                  │ scheduled tasks. │ Job metadata:...   
                   │                  │                  │                    
   app-job.yaml    │ Generate         │ Defines a Job    │  apiVersion: bat   
                   │ manifest         │ for running a    │ ch/v1 kind: Job    
                   │                  │ task to          │ metadata:...       
                   │                  │ completion.      │                    
   app-            │ Generate         │ Configures a     │  apiVersion: v1    
   livenessProbe.y │ manifest         │ liveness probe   │ kind: Pod metada   
   aml             │                  │ to check         │ ta:...             
                   │                  │ container        │                    
                   │                  │ health.          │                    
   app-            │ Generate         │ Defines a Pod    │  apiVersion: v1    
   multicontainer. │ manifest         │ with multiple    │ kind: Pod metada   
   yaml            │                  │ containers.      │ ta:...             
   app-            │ Generate         │ Configures a     │  apiVersion: v1    
   readinessProbe. │ manifest         │ readiness probe  │ kind: Pod metada   
   yaml            │                  │ to check if the  │ ta:...             
                   │                  │ app is ready.    │                    
   app-            │ Generate         │ Defines resource │  apiVersion: v1    
   resources.yaml  │ manifest         │ requests and     │ kind: Pod metada   
                   │                  │ limits.          │ ta:...             
   app-secret-     │ Generate         │ Uses Kubernetes  │  apiVersion: v1    
   env.yaml        │ manifest         │ Secrets as       │ kind: Pod metada   
                   │                  │ environment      │ ta:...             
                   │                  │ variables.       │                    
   app-            │ Generate         │ Defines volume   │  apiVersion: v1    
   volumeMounts.ya │ manifest         │ mounts for       │ kind: Pod metada   
   ml              │                  │ persistence.     │ ta:...             
   app.yaml        │ Generate         │ A basic          │  apiVersion: app   
                   │ manifest         │ application      │ s/v1 kind: Deplo   
                   │                  │ deployment       │ yment metadata:.   
                   │                  │ manifest.        │ ..     