Відділ маркетингу підготував анонс першого релізу продукту.

У цьому завданні потрібно створити новий Helm чарт з опціями по замовчуванню, запакувати чарт та створити новий реліз на GitHub. Рекомендується створити та протестувати інструкцію встановлення Helm пакету.

Dear Users,
We are excited to announce the first release of the bot-project! This release marks a significant milestone in our journey to provide multi-arch builds and support for Kubernetes installations.
To make it easier to deploy and manage, we have created a Helm chart that can be used to install and configure the application on Kubernetes clusters. The Helm chart includes all the necessary configurations and dependencies to get you up and running quickly.
In addition to the Helm chart, we have also created a GitHub release that includes the chart package, along with detailed release notes and instructions on how to deploy and use bot-project. This release is available now on our GitHub repository, and we encourage you to check it out.
<RELEASE-URL>
To get started, simply download the Helm chart package from the GitHub release page and use it to install the application on your Kubernetes cluster. You can also view the release notes for more information on new features, bug fixes, and other changes included in this release.
<INSTRUCTION>
Thank you for your support and happy deploying!

Best regards!
    
1. Створіть новий Helm чарт за допомогою команди (приклад розглядається на Coding Session):

helm create <CHART_NAME>
2. Підготуйте файл "values.yaml" у директорії чарту, включивши до нього блок:

image:
  repository: <REPO>
  tag: <TAG>
  arch: amd64
  
Додатково визначте секцію для токену TELE_TOKEN

3. Відредагуйте файл "deployment.yaml" у каталозі "templates" та додайте блок з посиланням на образ контейнеру:

spec:
  template:
    spec:
      containers:
        - name: {{ .Release.Name }}
          image: {{ .Values.image.repository }}/{{ .Chart.Name }}:{{ .Values.image.tag }}-{{ .Values.image.arch | default "amd64"}}
  
Додатково створіть блок для змінної середовища TELE_TOKEN із застосуванням Kubernetes secret

4. Запакуйте Helm чарт за допомогою команди:

helm package <dir>
  
5. Створіть новий реліз GitHub за допомогою інтерактивної команди GitHub CLI (вам може знадобитися GITHUB_TOKEN):

gh release create
  
6. Перевірте створений реліз командою:

gh release list
  
7. Додайте до релізу helm пакет:

gh release upload <RELEASE> <CHART_NAME>.tgz
  
8. Протестуйте Helm чарт, встановивши його за допомогою команди:

helm install <CHART_NAME> <CHART_URL>
  
9. Перевірте чи все необхідне вказано в інструкції та чарт встановлено і працює коректно.

10. Після виконання завдання обов'язково перегляньте і протестуйте Helm пакет, щоб переконатися, що все відповідає вимогам і функціонує коректно, додайте URL-адресу до HELM пакету релізу як відповідь.

Приклад формату відповіді: https://github.com/den-vasyliev/kbot/releases/download/v1.0.7/kbot-1.1.3.tgz