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