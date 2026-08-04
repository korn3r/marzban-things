Mod for https://github.com/gozargah/marzban

1. Clone original repo.
2. Replace files
3. docker build -t marz:0.1 . --network=host

__init__.py ---> Marzban/app/__init__.py  

requirements.txt ---> Marzban/requirements.txt  

Dockerfile ---> Marzban/Dockerfile  

subscription.py ---> Marzban/app/routers/subscription.py  

user.py ---> Marzban/app/routers/user.py


PS: Markdown invented for torturing people for sure
