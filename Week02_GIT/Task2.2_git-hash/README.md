Задача 2
Пройдіть невеликий челендж на увагу до деталей:
1.	Створіть нову директорію під контролем системи контролю версій Git.
mkdir new && cd new
2.	В директорії створіть файл з назвою challenge.txt
3.	Додайте до файлу текст: This is my Git challenge file.
echo "This is my Git challenge file." > challenge.txt
4.	За допомогою команди git хешуйте вміст файлу challenge.txt.
5.	Збережіть результат виконання команди у файлі з назвою hash.txt.
git hash-object -w challenge.txt > hash.txt
6.	Використайте системну команду git для відображення вмісту файлу challenge.txt, використовуючи хеш, збережений у файлі hash.txt та додайте вивід команди до hash.txt.
cat .\hash.txt
e712ae76a9167a62fd29c6956146688af2784529
git cat-file -p e712ae76a9167a62fd29c6956146688af2784529
or
git cat-file -p $(cat hash.txt) >> hash.txt
��This is my Git challenge file.
7.	Використовуйте команду update-index, щоб додати файл challenge.txt до індексу Git.
git update-index --add .\challenge.txt
8.	Використовуйте команду git ls-files, щоб переглянути staged вміст індексу Git. Результат додайте до hash.txt.
git ls-files -s >> .\hash.txt
Відповіддю на завдання буде вміст файлу hash.txt
cat .\hash.txt
e712ae76a9167a62fd29c6956146688af2784529
This is my Git challenge file.
100644 e712ae76a9167a62fd29c6956146688af2784529 0       challenge.txt
100644 4916f9cd2806d2c06d5f1e5f0e9fc7ee01350277 0       hash.txt
