### Знакомство с командной строкой

Чтобы вывести текущую рабочую директорию, можно использовать команду *pwd*.

У большинства пользователей компьютера есть доступ к домашней директории. Чтобы к ней перейти, используют команду *cd ~*.

### Навигация в командной строке

менять директории командой *cd*

выводить содержимое директорий с помощью *ls*;

просматривать содержимое вместе со скрытыми файлами и папками через *ls -a*

### Операции с файлами и папками: Создание, копирование, перемещение

Команда *touch* создаёт файл, а команда *mkdir* — директорию.

С помощью флага *-p* можно создать целую структуру директорий одной командой: *mkdir -p*.

Для копирования файлов используют команду *cp*, для перемещения — *mv*.

### Операции с папками и файлами: чтение и удаление

Вывести содержимое файла можно командой *cat*.

Для удаления файла используют *rm*, для удаления пустой директории — *rmdir*, а для директории с файлами — *rm -r*.

Все команды удаления стирают данные безвозвратно — их нельзя будет восстановить из корзины!

### Эффективная работа с командной строкой

С помощью *&&* можно выполнить несколько команд сразу — одну за другой.

Команды, которые вы выполняете в консоли, попадают в историю. Вы можете перемещаться по этой истории при помощи стрелок *↑↓*.

При нажатии на *Tab* консоль предложит несколько вариантов продолжения команды.

Символами */* и *~* можно быстро перемещаться к корневой и домашней директориям.


# Первый коммит

### Инициализируем репозиторий

Инициализировать репозиторий можно с помощью команды *git init*.

Проверить статус, или состояние, репозитория поможет команда *git status*.

Если вы ошиблись и случайно инициализировали не ту папку, можно «разгитить» её — удалить скрытую подпапку *.git*.

### Добавляем файлы в репозиторий

Команда *git add* позволяет подготовить файл к сохранению.

Команда *git add --all* подготовит к сохранению сразу все файлы.

С помощью *git add .* можно добавить в репозиторий текущую папку со всеми файлами.

### Делаем первый коммит

Коммит можно сделать с помощью команды *git commit*.

Ключ *-m* позволяет присвоить коммиту сообщение. Помните, что такие сообщения должны быть информативными: чётко описывать изменения.

В коммит попадает то, чтобы было предварительно добавлено «в корзину», или «в кадр», перед коммитом.

### Просматриваем историю коммитов

*git log* - Просмотреть историю коммитов

# Синхронизация репозиториев

### Что такое SSH. Генерируем SSH ключ

*SSH* — протокол, который обеспечивает безопасный обмен данными в сети и использует для этого ключи.

*SSH*-ключ — ваш виртуальный идентификатор в GitHub. Как ключ от квартиры, он позволяет получить доступ к GitHub-репозиторию. Также SSH используется для доступа к другим удалённым серверам.

*SSH*-ключ состоит из двух частей — публичной и приватной. Публичный ключ зашифрует данные, а приватный — расшифрует. Приватным ключом ни в коем случае нельзя делиться, иначе любой сможет расшифровать все ваши секреты!

Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду. *ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"*

### Привязываем SSH-ключ к GitHub

После выполнения команды ssh-keygen в директории *~/.ssh* будет создано два файла — *id_ed25519* и *id_ed25519.pub*

Выведите содержимое файла с помощью cat *~/.ssh/id_ed25519.pub* и скопируйте вывод в буфер обмена из консоли.

Перейдите на GitHub и выберите пункт Settings в меню аккаунта.

В меню слева нажмите на пункт SSH and GPG keys.

В открывшейся вкладке выберите New SSH key 

В поле Title (англ. «заголовок») напишите название ключа. Например, Personal key (англ. «личный ключ»).

В поле Key type (англ. «тип ключа») должно быть Authentication Key (англ. «ключ аутентификации»).

В поле Key скопируйте ваш ключ из буфера обмена.

Нажмите на кнопку Add SSH key

Проверьте правильность ключа с помощью следующей команды.

*ssh -T git@github.com*

### Связываем удаленный и локальный репозиторий

Перейдите на страницу удалённого репозитория, выберите тип *SSH* и скопируйте *URL*

Откройте консоль, перейдите в каталог локального репозитория и введите команду *git remote add origin git@github.com:%ИМЯ_АККАУНТА%/ИМЯ_ПРОЕКТА.git *

### Синхронизируем локальный и удалённый репозитории

Коммиты хранятся в ветках. Начальная ветка создаётся автоматически и называется main или master.

За отправку изменений на удалённый репозиторий отвечает команда *git push*. В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). 

Интерфейс GitHub позволяет удобно просмотреть все коммиты в репозитории, а также изменения в этих коммитах.

# Навигация по коммитам. Статусы файлов

### Хеш — идентификатор коммита

Git преобразует информацию о коммитах с помощью алгоритма SHA-1 и для каждого из них рассчитывает уникальный идентификатор — хеш.

Хеш — основной идентификатор коммита и позволяет узнать его автора, дату и содержимое закоммиченных файлов.

Все хеши, а также таблицу соответствий хеш → информация о коммите Git хранит в папке *.git*.

### Исследуем лог

Можно вызвать не только полный лог, но и сокращённый — это делается командой *git log --oneline*.

В сокращённом логе выводятся сокращённые хеши — их можно использовать точно так же, как и полные.

### HEAD — всему голова

В числе прочих файлов в папке *.git* есть служебный файл *HEAD*. Он указывает на самый свежий коммит.
Вместо хеша последнего коммита можно написать слово *HEAD* — Git вас поймёт.

### Статусы файлов в Git

Статусом *untracked* помечается файл, о существовании которого Git знает, но не следит за изменениями в нём. Этот статус — противоположность *tracked*, в который попадают все файлы, отслеживаемые Git.

Файл переходит в статус *staged* после выполнения git add.

Статус *modified* означает, что файл был изменён.

Большинство файлов в проектах «шагает» по следующему циклу: «изменён» → «добавлен в список на коммит» → «закоммичен» → «изменён» → и так далее.

### Как читать git status

Команда *git status* всегда подскажет, что происходит с файлом: например, он добавлен в список «на коммит» или ещё вообще не отслеживается, или изменён.

*git status* показывает явно следующие состояния файлов: *untracked*, *staged* и *modified*.

*git status* подсказывает, какие команды можно выполнить, чтобы поменять состояние файла.

# Работа над ошибками в коммитах

### Как исправить коммит

*--amend* рассчитан на работу с последним коммитом (HEAD).

Дополнить коммит новыми файлами можно с помощью *git commit --amend --no-edit*. Благодаря опции *--no-edit* сообщение к коммиту останется таким, каким и было.

Изменить сообщение к коммиту позволяет команда *git commit --amend -m "Обновлённое сообщение коммита"*.

### Как откатиться назад, если «всё сломалось»

Команда git restore --staged <file> переведёт файл из staged обратно в modified или untracked.

Команда git reset --hard <commit hash> «откатит» историю до коммита с хешем <hash>. Более поздние коммиты потеряются!

Команда git restore <file> «откатит» изменения в файле до последней сохранённой (в коммите или в staging) версии.

### Просматриваем изменения в файлах

Команда git diff сравнит последнюю закоммиченную версию файла с той, что находится в состоянии modified.

Команда git diff --staged покажет изменения в staged-файлах относительно последних закоммиченных версий.

### Сопостовляем коммиты

git diff! Эта команда поможет узнать, какие строки и в каких файлах изменились. Вы также познакомились с командой git diff <коммит1> <коммит2>. С её помощью удобно сравнивать изменения в двух коммитах.

*$ cat file.txt*
*Первая строка файла*
*$ echo "Новая строка" > file.txt*
*$ cat file.txt*
*Новая строка* 

*$ echo "Вторая строка файла" >> file.txt*
*$ cat file.txt*
*Первая строка файла*
*Вторая строка файла.*

### Игнорирование файлов в GIT

Если нужно, чтобы Git игнорировал какие-то файлы, стоит составить файл .gitignore.

Посмотреть, что игнорируется, можно с помощью команды git status --ignored.

Сам файл .gitignore — это обычный файл в репозитории. Его тоже стоит закоммитить.

Шаблонов много, но их легко найти в интернете вместе с примерами использования.

# Основы работы с ветками в git

### Клонируем репозитории

Команда git clone копирует проект на локальный компьютер.

git clone автоматически связывает локальный репозиторий с удалённым.


### Выполняем Fork

«Форк» позволяет получить точную копию GitHub-репозитория в ваш аккаунт.

Копия, которая получена с помощью «форка», полностью независима от оригинального проекта — изменения не будут синхронизированы.

# Ветки: создание, навигация, сравнение

### Что такое ветка

Ветка — это последовательность независимых изменений.

Благодаря веткам несколько человек могут работать над одним репозиторием и не мешать друг другу. А ещё ветки помогают декомпозировать большую и страшную задачу на маленькие и понятные.

Основная версия проекта хранится в главной ветке main (или master).

С помощью команды git branch можно посмотреть, какие в проекте есть ветки и в какой из них вы сейчас находитесь.

### Создаём ветку

Теперь вы умеете создавать ветки с помощью команды git branch <название_ветки>

### Шагаем с ветки на ветку

Команда git checkout <название_ветки> позволяет переключаться на другую ветку.

Разные ветки в одном проекте существуют независимо. Изменения в одной не влияют на изменения в другой.

В Git можно создать ветку и сразу же перейти в неё командой git checkout -b <название_ветки>.

Ветка указывает на коммит, который сделан в ней последним. При этом две ветки могут ссылаться на один и тот же коммит — например, если вы только что создали ветку, но ещё не успели внести в неё коммит.

### Сравниваем ветки

Потрясающе! В этом уроке вы узнали о ещё двух полезных функциях команды git diff. А именно:

git diff может сравнивать ветки по их названиям. Например, команда git diff main feature/my-feature выведет разницу между основной веткой и веткой feature/my-feature.

Git поддерживает суффикс навигации ~. С его помощью можно сослаться на предыдущие коммиты. Например, если вы находитесь в ветке main и хотите вывести разницу между тем коммитом, который был три коммита назад, и текущим, нужно выполнить git diff main~3 main.

# Слияние и удаление веток

### Объединяем и удаляем ветки

Поздравляем! Теперь вы понимаете, как работает ветвление в Git. Что важно запомнить:

Выполнить слияние веток позволяет команда git merge <название_ветки>. В качестве параметра указывают название ветки, которую нужно влить в текущую.

Удалять ненужные ветки после слияния — хорошая практика. Так в вашем репозитории всегда будет порядок. За удаление веток отвечает команда git branch -D <название_ветки> и её щадящий вариант с флагом -d.

# Работа с ветками в удалённом репозитории

### Создаём pull request

Пул-реквест — это запрос на рассмотрение предлагаемых изменений и часть процесса ревью.

Запрос на изменения можно инициировать двумя способами: через ссылку, которую Git выводит после создания ветки, или через интерфейс GitHub.

После создания пул-реквеста ваши коллеги сделают ревью — оценят предложенные вами правки и оставят свои комментарии.

По результатам ревью ваши правки могут быть приняты в основную ветку проекта или возвращены на доработку.

### Забираем изменения из удалённого репозитория

Прекрасно! В этом уроке вы научились загружать изменения из удалённого репозитория на свой локальный компьютер. Подытожим:

Команда git pull позволяет подтянуть изменения из удалённого репозитория в локальный.

Перед созданием нового пул-реквеста считается хорошей практикой перейти в главную ветку, «подтянуть» в неё изменения, а затем добавить эти изменения в вашу ветку с помощью git merge main.

# Продвинутая командная работа с Git

# Работа с ветками на практике

### Что такое fast-forward

Если истории двух веток не «разошлись» и их коммиты выстраиваются в одну цепочку, эти ветки можно объединить в режиме fast-forward.

Режим fast-forward можно отключить с помощью флага --no-ff.

### Non-fast-forward

Если истории двух веток всё же «разошлись», при слиянии веток Git создаст коммит слияния.

При объединении веток в состоянии не-fast-forward возможны (но не обязательны) конфликты. Если конфликты всё же возникли, Git попытается разрешить их самостоятельно или попросит вас сделать это вручную.

### git push и fast-forward

### Почему бы не «пушить» всё в main

### Модели веток. Простая feature branch модель