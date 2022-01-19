# evernote-example
Набор скриптов для работы с сервисом Evernote через API.

## Как установить
Скопируйте репозиторий к себе на компьютер:
```
git clone https://github.com/clownkill/evernote-example
```
Python 2.7 должен быть установлен. Затем используйте pip для установки зависимостей:
```
pip install -r requirements.txt
```

## Настройка. Объявление переменных окружения
Перед запуском скриптов в одном каталоге со скриптами необходимо создать файл для хранения переменных
окружения с именем `.env` и следующим содержимым:
```
EVERNOTE_CONSUMER_KEY=[KEY]
EVERNOTE_CONSUMER_SECRET=[SECRET]
EVERNOTE_PERSONAL_TOKEN=[TOKEN]
JOURNAL_TEMPLATE_NOTE_GUID=[GUID]
JOURNAL_NOTEBOOK_GUID=[GUID]
INBOX_NOTEBOOK_GUID=[GUID]
```
Где:
- EVERNOTE_CONSUMER_KEY - ваш consumer key, нужно получить при регистрации на [dev.evernote.com](https://dev.evernote.com/#apikey).
- EVERNOTE_CONSUMER_SECRET - ваш consumer secret, нужно получить при регистрации на [dev.evernote.com](https://dev.evernote.com/#apikey).
- EVERNOTE_PERSONAL_TOKEN - ваш ключ разработчика, нужно получить на сайте [evernote](https://www.evernote.com/Login.action?targetUrl=%2Fapi%2FDeveloperToken.action).
- JOURNAL_TEMPLATE_NOTE_GUID - GUID заметки, которая в дальнейшем будет использоваться как шаблон. 
- JOURNAL_NOTEBOOK_GUID - GUID блокнота для заметок, которые генерируются автоматически.
- INBOX_NOTEBOOK_GUID - GUID блокнота, являющегося ящиком для входящих сообщений.

## Описание скриптов
### list_notebooks.py
Скрипт делает запрос к API Evernote и выводит в консоль список всех блокнотов (GUID и заголовок) хранящихся в аккаунте.

### dump_inbox.py
Выводит список заметок, которые хранятся в блокноте - ящике для входящих сообщений. GUID блокнота `INBOX_NOTEBOOK_GUID`
хранится в .env.

По умолчанию в консоль выводится 10 последних заметок. При запуске скрипта ему можно передать необходимое
для вывода количество заметок с помощью аргумента:
```
python dump_inbox.py [количество заметок]
```

### add_note2journal.py
Создает запись по шаблону `JOURNAL_TEMPLATE_NOTE_GUID` и сохраняет ее в блокноте, указанном в `JOURNAL_NOTEBOOK_GUID`.

Заголовок шаблона должен содержать места для вставки даты и дня недели, например `{date}--{dow}`.
По умолчанию в заголовок вставляются текущие системные дата и время. В случае, если необходимо установить
другие дату и время их необходимо передать в ISO-формате(YYYY-MM-DD) как аргумент при вызове скрипта:
```
python add_note2journal.py [YYYY-MM-DD]
```

## Цель проекта
Код написан в образовательных целях на онлайн-курсе [Dvmn.org](https://dvmn.org/).