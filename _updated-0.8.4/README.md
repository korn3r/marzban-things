Скачать готовый image: https://github.com/korn3r/marzban-things/releases/tag/v1-beta.3  

Mod for https://github.com/gozargah/marzban

1. Clone original repo.
2. Replace files
3. docker build -t marz:0.1 . --network=host

__init__.py ---> Marzban/app/__init__.py  
requirements.txt ---> Marzban/requirements.txt  
Dockerfile ---> Marzban/Dockerfile  
subscription.py ---> Marzban/app/routers/subscription.py  
user.py ---> Marzban/app/routers/user.py  
v2ray.py ---> Marzban/app/subscription/v2ray.py  
xray-config.py ---> Marzban/app/xray/config.py  
config.py ---> Marzban/config.py

PS: Markdown invented for torturing people for sure  



Основные изменения:   
ОС - Alpine  
Обновлены некоторые компоненты.  
Пофикшена совместимость с некоторыми новыми библиотеками (например в свежем fastapi поменялся способ итерации...)  
Убрана отправка заголовков extra в xHTTP - Марзбан все равно шлет дефолтные параметры ядра, так что можно и не слать их вообще.  
Убрана отправка поля email.  
Добавлена поддержка VLESS Encryption:  
Нужно в .env вписать VLESS_ENC={ключ encryption} и в конфиге ядра нужно вписать ключ decryption ("decryption" = "{ключ}")  
В подписке в заголовке profile-web-page-url адрес сервера теперь тот что указан в XRAY_SUBSCRIPTION_URL_PREFIX
