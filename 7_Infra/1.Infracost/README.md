Під час конференції Kubecon я зустрівся з представником Infracost, який надав мені корисні поради та інструкції щодо використання їхнього продукту для оцінки витрат на проєкти.

**Infracost** — це інструмент для оцінки витрат на хмарні технології, який допомагає розробникам та командам DevOps краще розуміти та управляти витратами, пов'язаними з cloud-інфраструктурою.

Виконавши це завдання, ви зможете забезпечити моніторинг та управління змінами вашої інфраструктури з метою економічної ефективності та результативності.

**Завдання включає:**

fork Git-репозиторію;
перевірку конфігурації Terraform;
встановлення та автентифікацію Infracost;
налаштування протекту основної гілки;
налаштування інтеграції з Infracost;
тестування змін за допомогою pull-request .
Приклад виконання:

1. Почніть з форку репозиторію з terraform кодом: https://github.com/den-vasyliev/tf-google-gke-cluster. Це створить копію репозиторію у вашому власному акаунті GitHub, з яким ви зможете працювати та змінювати локально.
2. Перевірте конфігурацію Terraform: за допомогою Google Cloud Shell перейдіть до репозиторію і запустіть terraform init, terraform validate і terraform plan, щоб перевірити конфігурацію Terraform на наявність помилок і переконатися, що план правильний.
3. Встановіть Infracost в Google Cloud Shell: curl -fsSL https://raw.githubusercontent.com/infracost/infracost/master/scripts/install.sh | sh
4. Авторизуйтеся в Infracost, запустивши infracost auth login.
5. Увімкніть захист гілки main, щоб запобігти випадковим змінам або несанкціонованим модифікаціям.
6. Додайте інтеграцію Infracost до репозиторію, дотримуючись інструкцій https://www.infracost.io/docs/. Це дозволить вам автоматично розраховувати і контролювати витрати на інфраструктуру при внесенні змін до сховища.
7. Створіть pull-request на внесення змін до коду terraform, наприклад, кількість та тип нод у кластері і протестуйте зміни, щоб переконатися, що все працює належним чином.  
**Відповідь:**  
Посилання на PR, приклад https://github.com/den-vasyliev/tf-google-gke-cluster/pull/1

# Налаштування інструменту оцінки витрат на хмарні технології **Infracost** 

1. fork Git-репозиторію: https://github.com/den-vasyliev/tf-google-gke-cluster
- Все робиться в Web на GitHUBі

2. Виконаємо перевірку конфігурації Terraform;
- Заходимо Google Cloud Shell
- Клонуємо форкнутий репозиторій 
- Запускаємо команди для перевірки з консолі:
```sh
✗ terraform init
Terraform has been successfully initialized!

✗ terraform validate
Success! The configuration is valid.

✗ terraform plan
Plan: 3 to add, 0 to change, 0 to destroy.
```
3. Встановимо та пройдемо автентифікацію [Infracost](https://www.infracost.io/docs/)
```sh
✗ curl -fsSL https://raw.githubusercontent.com/infracost/infracost/master/scripts/install.sh | sh
Completed installing Infracost v0.10.31
```
- зареєструємось на сайті https://dashboard.infracost.io/org/umanetsvitaliy:
```
1. Select your source control system
2. Connect your source control system
Your application is connected
3. Add your code repos
4. Configure private module access
```
- Переходимо в лівому верхньому куті головного меню `Org Settings` -> `General`-> `API Key` та копіюємо ключ
```sh
✗ read -s INFRACOST_API_KEY
✗ echo $INFRACOST_API_KEY
✗ infracost configure set api_key $INFRACOST_API_KEY

✗ infracost breakdown --path .
2023-12-14T21:42:52Z INF Enabled policies V2
2023-12-14T21:42:52Z INF Enabled tag policies
Evaluating Terraform directory at .
  ✔ Downloading Terraform modules 
  ✔ Evaluating Terraform directory 
  ✔ Retrieving cloud prices to calculate costs 

Project: vit-um/tf-google-gke-cluster

 Name                                                 Monthly Qty  Unit   Monthly Cost 
                                                                                       
 google_container_cluster.this                                                         
 └─ Cluster management fee                                    730  hours        $73.00 
                                                                                       
 google_container_node_pool.this                                                       
 ├─ Instance usage (Linux/UNIX, on-demand, g1-small)        1,460  hours        $26.27 
 └─ Standard provisioned storage (pd-standard)                200  GB            $8.00 
                                                                                       
 OVERALL TOTAL                                                                 $107.27 
──────────────────────────────────
2 cloud resources were detected:
∙ 2 were estimated, all of which include usage-based costs, see https://infracost.io/usage-file

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━┓
┃ Project                                            ┃ Monthly cost ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━┫
┃ vit-um/tf-google-gke-cluster                       ┃ $107         ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━┛
```

4. Налаштування проекту основної гілки
- На гітхабі в клонованому репозиторії заходимо в налаштування, в лівому меню `Branches` та обираємо `Require a pull request before merging`   


5. Налаштування інтеграції з Infracost робимо прямо на сайті за допомогою майстра налаштувань

6. Тестування змін за допомогою pull-request
- В консолі:
```sh
git checkout -b dev
git add .
git commit -m"node =5"
[dev 9395585] node =5
 2 files changed, 2 insertions(+), 2 deletions(-)

git push origin dev
```
- На гітхабі створюємо pull-request з dev в main та отримуємо прямо в запиті наступне повідомлення від Infracost:

Infracost report
💰 Monthly cost will decrease by $34 📉
Project	Cost change	New monthly cost
vit-um/tf-google-gke-cluster	-$34 (-22%)	$124