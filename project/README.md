<h1 align="center">Telegram-bot Hotel finder

[![Telegram URL](https://www.dampftbeidir.de/mediafiles/tpl/icon-telegram.png)](https://t.me/sejeenn_bot) 
</h1>

***

## Краткое описание

Телеграм-бот позволяет найти выгодное предложение на платформе [Hotels.com](https://hotels.com/).
<br> Пользователь с помощью специальных команд бота может выполнить следующие действия (получить следующую информацию): <br/>
- Узнать топ самых дешёвых отелей в городе (**команда /lowprice**). 
- Узнать топ самых дорогих отелей в городе (**команда /highprice**). 
- Узнать топ отелей, наиболее подходящих по цене и расположению от центра (самые дешёвые и находятся ближе всего к центру) (**команда /bestdeal**). 
- Узнать историю поиска отелей (**команда /history**)


**Для разработки и функционирования проекта используется открытый API Hotels, который расположен на сайте [rapidapi.com](https://rapidapi.com/apidojo/api/hotels4/).**

***

## Как запустить бот:
- Скачать скрипт и распаковать архив
- Установить зависимости: `pip install -r requirements.txt`
- Создать telegram-бота у [BotFather](https://t.me/BotFather) и получить токен
- Получить ключ от rapidapi:
    - Зарегистрироваться на сайте [rapidapi.com](https://rapidapi.com/apidojo/api/hotels4/)
    - Перейти в API Marketplace → категория Travel → Hotels (либо просто перейти по прямой ссылке на документацию [Hotels API Documentation](https://rapidapi.com/apidojo/api/hotels4/))
    - Нажать кнопку **Subscribe to Test**
    - Выбрать пакет (есть бесплатный вариант)
    - Забрать KEY
- Создать файл **.env** и прописать там BOT_TOKEN и RAPID_API_KEY так, как это представленно в файле-шаблоне .env.template
- Запустить бота: `python main.py`

***

## Принцип работы бота

После ввода команд **/lowprice** и **/highprice** бот проводит опрос пользователя:
- город поиска
- количество отелей для вывода результата (максимум 10)
- нужно ли загрузить фото отеля
- если да, то количество фото (максимум 10)
- дата заселения в отель и дата выселения


При вводе команды **/bestdeal** дополнительно запрашивается:
- диапазон цен в $ за 1 ночь
- диапозон удаленности от центра города в км


При удачных запросах ведется история поиска. Все запросы и их результат сохраняются в базе данных.

При вводе команды **/history** пользователю предлагается уточнить действие:
- Показать историю поиска — будет показана вся история поисковых запросов пользователя. При нажатии на конкретный запрос выводится результат того поиска.
- Очистить историю — вся история поиска будет удалена из базы данных.

***

## Описание внешнего вида и UI
Окно Telegram-бота при запущенном Python-скрипте воспринимает следующие команды:
- **/start** - запуск бота и приветствие
- **/help** — помощь по командам бота 
- **/lowprice** — вывод самых дешёвых отелей в городе
- **/highprice** — вывод самых дорогих отелей в городе 
- **/bestdeal** — вывод отелей, наиболее подходящих по цене и расположению от центра
- **/history** — вывод истории поиска отелей

Для команд **/lowprice**, **/highprice** и **/bestdeal** сообщение с результатом содержит краткую информацию по каждому отелю. 
В эту информацию входит: 
- Название отеля
- Как далеко отель расположен от центра (в км)
- Цена за ночь (в долларах США)
- Стоимость за N ночей (в долларах США)
- Адрес отеля
- N фотографий отеля (если пользователь счёл необходимым их вывод)
