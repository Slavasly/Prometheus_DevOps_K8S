# new-project
DevOps by Kubernetes from Prometheus
=======
Jira Ticket: PROM-42164:

Task Title: Set up new Git repository and create development branch for 'new-project'

Task Description:

As a developer, I need a new GitHub repository for 'new-project' and i need a development branch so that I can work on new features without affecting the main branch. 
Readme file should contain step-by-step instructions on how we can do it ourselves.

Expected Results:

A new branch called "development" is created and the user is able to switch to it successfully.

A new file called "README.md" is created and step-by-step instructions is added to it successfully.
The changes to the "development" branch are committed with a commit message successfully.
The changes from the "development" branch are merged into the "main" branch successfully.


Definition of Done (DoD):
1.Створіть в своєму середовищі новий каталог з назвою "new-project".
2.Перейдіть до каталогу "new-project". 
cd .\new-project\

3.Ініціалізуйте новий публічний Git-репозиторій всередині каталогу "new-project".
Demo\new-project> git init

4.Створіть новий файл з назвою "README.md" і додайте до нього початковий текст.
5.Підготуйте файл "README.md" до коміту.
Demo\new-project> git add .

6.Закомітьте зміни у репозиторій з коміт повідомленням “init”.
Demo\new-project> git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md

new-project> git commit -m "init"
[main (root-commit) 206b6d8] init
 1 file changed, 20 insertions(+)
 create mode 100644 README.md

7.Створіть нову гілку з назвою "development" і перейдіть до неї.
Demo\new-project> git checkout -b development
Switched to a new branch 'development'

8.Додайте інструкцію до файлу "README.md" і підготуйте їх до коміту.
 git add . 
PS C:\Users\sly\Downloads\DevOps\Prometheus\Demo\new-project> git status
On branch development
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

9.Закомітьте зміни у гілці "development" з повідомленням у форматі Smart Commit (див. інструкцію https://support.atlassian.com/jira-software-cloud/docs/process-issues-with-smart-commits/#Smart-Commit-commands) .
Demo\new-project> git commit -m "Jira Ticket: PROM-42164 #comment updated Readme.mdcomment #time 1h 10m Total work logged"
[development 512e1e0] Jira Ticket: PROM-42164 #comment updated Readme.mdcomment #time 1h 10m Total work logged
 1 file changed, 37 insertions(+), 2 deletions(-)

10.Об'єднайте зміни з гілки "development" у гілку "main".
Demo\new-project> git branch
* development
  main
PS C:\Users\sly\Downloads\DevOps\Prometheus\Demo\new-project> git checkout main
Switched to branch 'main'
PS C:\Users\sly\Downloads\DevOps\Prometheus\Demo\new-project> git merge development
Updating 206b6d8..512e1e0
Fast-forward
 README.md | 39 +++++++++++++++++++++++++++++++++++++--
 1 file changed, 37 insertions(+), 2 deletions(-)

11.Перевірте статус, переконайтеся, що все актуально.
Demo\new-project> git status
On branch main
nothing to commit, working tree clean

11.Link to new-project Readme file

ON BRANCH DEVELOPMENT
