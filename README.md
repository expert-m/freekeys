FreeKeys CMS – специальный движок позволяющий создать сайт для раздачи ключей, предметов и прочего. С версии 1.5 движок ориентирован не только под раздачу ключей для игр, но и для других программ, предметов. В базе данных уже присутствуют несколько игр для демонстрации.

##### Как же он работает?
1. Пользователь регистрируется.
2. Зарабатывает баллы размещая свою реферальную ссылку и приглашая друзей.
3. Покупает на собранные баллы предметы.

---

### Навигация
**[Установка](#Установка)**<bк>
**[Настройки](#Настройки)**<bк>
**[Шаблоны](#Шаблоны)**<bк>
**[Задания](#Задания)**<bк>
**[Ключи](#Ключи)**<bк>
**[Локализация](#Локализация)**<bк>
**[Интерфейсы](#Интерфейсы)**<bк>
**[Плагины](#Плагины)**

### Установка
1. Скачайте архив и распакуйте его в нужно место.
2. Установите для папки "cache" права на запись (CHMOD 777).
3. Установите для "config.json" права на запись (CHMOD 777).
4. Файл "MySQL.sql" из архива импортируйте в свою базу данных.
5. [Настройте](#Настройки) "config.json", указав там данные для входа в базу данных.

##### Данные для входа в админ-панель (/admin.php)
* Логин: admin
* Пароль: 1111

##### Инструкция по подключению ВКонтакте авторизации
1. Создайте свое приложение (http://vk.com/editapp?act=create) типа Standalone-приложение.
2. В настройках приложения укажите свой адрес сайта (например: http://nextable.ru/) .
3. ID приложения и защищенный ключ из настроек приложения скопируйте в настройки сайта.

##### Инструкция по подключению Facebook авторизации
1. Зайдите на https://developers.facebook.com/apps , нажмите "Create a New App", в поле "Display Name" укажите имя приложения, выберите любую категорию и создайте приложение.
2. Зайдите в "Settings", нажмите "Add Platform" и выберите "Website".
3. В поле "App Domains" введите адрес своего сайта (например: http://nextable.ru/).
4. ID приложения и защищенный ключ из настроек скопируйте в настройки сайта.

### Настройки
Все основные настройки содержаться в файле "config.json".
Информация о формате JSON: https://ru.wikipedia.org/wiki/JSON

##### База данных
* db_name – имя базы данных
* db_user – пользователь базы данных
* db_password – пароль для входа в базу данных
* db_host - хост
* db_prefix – префикс таблиц

##### ВКонтакте
* auth_vk – разрешить или запретить авторизацию через ВКонтакте (true, false)
* auth_vk_app_id – ID приложения для авторизации
* auth_vk_app_secret – секретный ключ приложения 

##### Facebook
* auth_facebook - разрешить или запретить авторизацию через Facebook (true, false)
* auth_facebook_app_id – ID приложения для авторизации
* auth_facebook_app_secret – секретный ключ приложения 

##### Предметы
* items_reg_points – количество поинтов выдаваемых при регистрации
* items_ref_limit – количество засчитываемых пользователей перешедших по ссылке за 1 час
* items_ref_cost – стоимость перехода по ссылке
* items_ref_reg_cost – стоимость регистрации по ссылке

##### Остальное 
* home_url – адрес сайта (например: http://nextable.ru)
* list_plugins – список плагинов
* lang - язык (например "ru_RU" или "en_EN")
* timezone - часовой пояс (http://php.net/manual/ru/timezones.php)
* auth_online – время онлайна в секундах

### Шаблоны
С версии 1.5 используется обработчик шаблонов Twig (http://twig.sensiolabs.org/).

Перед созданием/редактированием шаблона ознакомитесь с Twig:
* http://twig.sensiolabs.org/doc/templates.html (на английском) 
* http://x-twig.ru/for_template_designers/ (на русском)

Все шаблоны находятся в папке "themes".

##### Описание файлов шаблона "default"
* 404.twig – страница ошибки 404
* banner_1.twig – левый баннер
* banner_2.twig – правый баннер
* base.twig - базовый шаблон
* edit_profile.twig – страница редактирования профиля
* error.twig – страница фатальной ошибки 
* index.twig – главная страница
* item.twig – описание предмета
* items.twig – список предметов
* key.twig – страница получения ключа
* main.php – главный файл. Отвечает за отображения сайта (что и на каких страницах выводить).
* messages.twig – список сообщений
* profile.twig – профиль пользователя
* ref.twig – реферальная страница
* register.twig – страница регистрации
* tasks.twig – список заданий


### Задания
#### vk_likes
Проверяет сделал ли пользователь репост или поставил лайк.

Параметры:
##### type

###### Возможные значения:
* post — запись на стене пользователя или группы;
* comment — комментарий к записи на стене;
* photo — фотография;
* audio — аудиозапись;
* video — видеозапись;
* note — заметка;
* photo_comment — комментарий к фотографии;
* video_comment — комментарий к видеозаписи;
* topic_comment — комментарий в обсуждении;
* sitepage — страница сайта, на котором установлен виджет «Мне нравится».

##### owner_id
Укзаельца Like-объекта: id пользователя, id сообщества (со знаком «минус») или id приложения. Если параметр type равен sitepage, то в качестве owner_id необходимо передавать id приложения. Если параметр не задан, то считается, что он равен либо идентификатору текущего пользователя, либо идентификатору текущего приложения (если type равен sitepage).

##### item_id
Идентификатор Like-объекта. Если type равен sitepage, то параметр item_id может содержать значение параметра page_id, используемый при инициализации виджета «Мне нравится».

##### filter
Указывает, следует ли вернуть всех пользователей, добавивших объект в список "Мне нравится" или только тех, которые рассказали о нем друзьям. Параметр может принимать следующие значения: 
* likes — возвращать информацию обо всех пользователях; 
* copies — возвращать информацию только о пользователях, рассказавших об объекте друзьям.
По умолчанию возвращается информация обо всех пользователях. 

###### Пример
```json
{"type": "post", "owner_id": "1", "item_id": "45651", "filter": "likes"}
```

Дополнительная информация: http://vk.com/dev/likes.getList

##### vk_groups_is
Проверяет является ли пользователь участником сообщества.

Параметры:
* group_id - идентификатор или короткое имя сообщества

###### Пример
```json
{"group_id": 57569441}
```
Дополнительная информация: http://vk.com/dev/groups.isMember

### Ключи
###### Ключи имеют 5 основных параметра
* Ключ 
* Инструкция
* Дополнительная информация
* Количество
* Проинформировать администратора (да/нет)

##### Получается 3 режима
1. Указан ключ и количество.
Пользователь получает ключ так же как и в FreeKeys 1.3 
2. Указана инструкция
Пользователь в данном случае следует Вашим указаниям. Например, зайти на сайт мой_сайт.ру и ввести свой id
3. Указана инструкция или доп. информация и информирование администратора.
В этом случае пользователь ожидает пока администратор обработает запрос и вышлет ему ключ 

### Локализация
Для перевода определенного плагина/шаблона требуется в его папке создать файл "locale/(язык)/LC_MESSAGES/lang.mo".

###### PHP функции для перевода
* set_lang_name(имя_ плагина) – получает перевод плагина
* __(текст, имя_ плагина) – переводит текст
Если требуется перевести шаблон, то вместо «имя_ плагина» указываем «tpl»
* _n() – синоним стандартной функции ngettext()
* _s(текст, параметр1, параметр2, …) – переводит текст и потом форматирует его через функцию sprintf()

###### Пример использования:
```php
__('Unknown error.');
_s('Account or IP banned until %s.', date('H:i:s, d.m.Y'));
```

Для редактирования *.po файлов можете использовать Poedit.

###### Создание/обновление lang.po файлов плагина/шаблона:
http://твой_сайт/modules/locale/parse.php?type=(module или theme)&name=(название плагина или шаблона)&action=(update или оставляем параметр пустым)&lang=(язык если нужно обновить)

###### Пример использования
```
http://твой_сайт/modules/locale/parse.php?type=theme&name=admin – создает файл перевода для шаблона "admin"
http://твой_сайт/modules/locale/parse.php?type=module&name=auth&action=update&lang=ru_RU – обновляет/дополняет новыми значениями русский перевод плагина «auth»
```

### Интерфейсы
С помощью интерфейсов можно вызывать функции и методы в шаблоне, через POST запросы и т.д.

##### Для вызова интерфейса нужно передать в функцию "interface" 3 параметра:
1. Категория/название плагина
2. Название функции
3. Массив параметров

##### Список интерфейсов
* auth - авторизация
 * login - вход
 * logout - выход
 * register - регистрация
 * save_profile - сохранение профиля
* message - сообщения
 * add - добавляет сообщение
 * get_messages - получает сообщения

##### Пример вызов интерфейса из PHP
```php
$tpl->add_function('get_item', $me->get_interface('items', 'get'));
```

##### Пример вызов интерфейса из HTML с помощью POST запроса
```html
<input class="form-control" name="interface[items][save_task][0][type]" value="vk_is" type="text">
<button name="interface[items][save_task][0][run]" type="submit" class="btn btn-success btn-lg">Save</button>
```

Для выполнения интерфейса нужно указать
```
interface[items][save_task][0][run]
```

Как видно после interface[items][save_task] идет [0]. Это используется для того чтобы можно было вызывать несколько раз один и тот же интерфейс.

##### Пример 
```html
<input class="form-control" name="interface[items][save_task][0][type]" value="vk_is" type="text">
<button name="interface[items][save_task][0][run]" type="submit" class="btn btn-success btn-lg">Save</button>

<input class="form-control" name="interface[items][save_task][1][type]" value="vk_is" type="text">
<button name="interface[items][save_task][1][run]" type="submit" class="btn btn-success btn-lg">Save</button>
```

### Плагины
##### Инструкция по созданию плагина:
1. В папке "plugins" создается новую папку с название модуля (например: "my_module").
2. Теперь заходим в созданную папку (plugins/my_module) и создаем php файл с названием модуля (my_module.php).
3. Заходим в файл "config.json" и в "list_plugins" добавляем название нового модуля.

##### Функции и методы, которые можно использовать в плагине 
* $me->config(название_переменной, default_значение) - получение настроек
 * Список настроек
  * auth - авторизирован ли пользователь (true/false)
  * level - уровень пользователя
  * user - массив с данными о пользователе
  * И все остальные настройки из config.json
* $me->set_config(название_переменной, значение) - устанавливает настройки
* captcha(id, код) - сравнивает полученный код с оригинальным
* File::get_contents(url) - cиноним функции file_get_contents()
* Log::add(text, tag) - добавлет сообщение в лог
* Log::get(key, where) - получает лог
* Log::getCount(key, arg) - получает количество логов
* Mail::send(arg) - отправляет соощение на email
* SmartDB::get() - синоним $db->get() только в конце форматирует результат
* SmartDB::getOne() - синоним $db->getOne() только в конце форматирует результат
* User::ban(время_бана) - блокировка пользователя на определенный период
* User::isBan() - проверка заблокирован пользователь или нет
* UserMeta::add(arg) - добавляет дополнительную информацию для пользователя 
* UserMeta::get(key, id', ip) - получает информацию
* UserMeta::delete(id) - удаляет
* Message - смотрите интерфейсы
* $db - смотрите https://github.com/joshcam/PHP-MySQLi-Database-Class
* $tpl->add_function($name, $func = '') - добавляет функцию в шаблон
* $tpl->add_filter($func, $name = '') - добавляет фильтер в шаблон
* $tpl->add_variable($tag, $value) - добавляет переменную в шаблон

##### Actions
* auth_register - вызывается при регистрации (можно изменить "user" из настроек)
* auth_end_init - конец авторизации 

---

### Поддержка проекта

##### WebMoney кошельки
* R403406801880
* Z198687614813
* U306139830046
* E426424497618

Большое спасибо тем, кто помогает проекту.
