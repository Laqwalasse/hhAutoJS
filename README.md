# JobuxAuto
Скрипт в формате автотеста, который автоматически откликается на вакансии по заданным параметрам.

Гифка "зависает" на этапе пагинации, нужно подождать ~15 сек (сейчас этой проблемы уже нет, но перезаписывать лень). На релевантность вакансий не смотрим, тут просто показ, как работает скрипт.

![JobuxAuto](https://github.com/user-attachments/assets/09046e2c-ee60-4481-9168-dec69087874a)

## Как использовать
1. Скачиваем этот репозиторий
2. Жмём комбинацию `win + R`
3. В открывшемся окне пишем `cmd`
4. Переходим в директорию, куда скачали репозиторий через команду `cd`. Например: `cd C:\Users\User\Downloads`
5. Пишем `npm start`
6. В открывшемся интерфейсе заполняем свои параметры, аналогично примерам. То же самое можно сделать вручную, открыв файл "settings.txt" в папке репозитория. Login и Password сейчас заполнять не нужно, они под виртуалку node.js, которая сейчас не готова.
![image](https://github.com/user-attachments/assets/7a233d32-4d80-4190-b8c7-a32f23a22a0f)
Сейчас там все параметры стоят на поиск по всему миру и в сфере айти. Чтобы поменять надо открывать хедхантер, перейти в расширенный поиск и открыть нужный раздел. Затем по конкретному пункту кликнуть правой кнопкой мыши и выбрать "Inspect". Откроется devtools и в нём нужно найти цифру этого элемента. На примере изображения это будет "47" для нефтегаза.
![image](https://github.com/user-attachments/assets/fb37f1b8-441c-4e0b-8e97-2826a559c7ce)
8. Жмём кнопку "Запустить"

## Предыстория
Когда-то я тратил по несколько часов в день на просмотр вакансий с hh. Переделывал несчетное количество раз резюме под разные форматы, пытался выстрелить на уровне SEO.

В результате из всех попыток:
- Более чем в половине случаев рекрутеры сами не знают, кого ищут: название вакансии — бизнес-аналитик, описание вакансии полностью под системного, на скрининге рекрутер задаёт вопросы про бизнес/системный, а на техническом выясняется, что ищут продуктового.
- Большая часть откликов получает отказ за промежуток до 10 секунд после того, как рекрутер зашёл в резюме. Исходя из статей и ютуб видео от самих рекрутеров, причиной этому является то, что эти "специалисты" проверяют резюме через ctrl+F на ключевые слова или могут дропнуть не проверяя, просто потому что им сходу ничего не понятно и разбираться они не хотят *roflanEbalo*.
- Ещё некоторое количество рекрутеров используют автоматизированное ПО, ботов, опросники. Думаю всем понятно, что через бота можно не пройти на конкурс просто не попав в его референсы для ответов.
- Абсолютно нулевой фидбек после скрининга/технического и тестовых заданий.

Очевидно, что пытаться вникать и адекватно искать подходящие по описанию тебе вакансии при таких условиях — пустая трата времени, за которое тебе ещё и не платят, в отличии от рекрутеров. 

В один день я психанул и откликнулся просто на всё подряд, что было в предложке, и внезапно — это дало хоть какой-то результат.

После этого я задался целью написать скрипт, который будет ещё и откликаться за меня, так как я ненавижу рутину, которую можно избежать.

## Текущее состояние
Реализация через автотест очень плохая сама по себе. hh выпуская обновления ломает скрипту обе ноги, производительность падает кратно. 

Сначала я с этим мирился, потому что очень не хотел завязываться на их API и токене, так как потенциально они могут перестать мне их предоставлять и я в итоге всё равно вернусь к автотесту.

Но на текущий момент 1 раз прогнать квоту 200 откликов в день занимает от 40 до 90 минут (раньше занимало не более получаса, но, опять же, обновления от hh... позже попробую разобраться). Там есть минимальные условия по прогрузке селекторов и обходу DDoS, из-за которых даже теоретически нельзя сделать быстрее, чем ~20 минут.

В итоге я решил, что максимально оформлю этот репозиторий (добавлю how-to, оформлю и раскидаю таски в гитхаб раздел "Issues", полное описание), сделаю MVP, а потом заморожу и начну делать ту же задумку, но через полноценное API.  

За качество кода прошу простить. Я бизнес-аналитик, с программированием ни по образованию, ни по работе никак не связан. В целом не преследую цели писать "хороший" код, мне на текущий момент важно реализовать функционал, оптимизация уже потом.

## Примечание

- **node.js** должен быть скачан и установлен. Ссылка: **https://nodejs.org/en**
- **ChromeDriver** должен быть скачан и установлен. Ссылка: **https://googlechromelabs.github.io/chrome-for-testing/**
- **Браузер по умолчанию**: Google Chrome (в других браузерах селекторы могут работать некорректно). Ссылка: **https://www.google.com/intl/ru_ru/chrome/**
- **ОС**: тестировал на Windows 10. За остальные сказать не могу.
- **Сломанные вакансии**: иногда встречаются отдельные вакансии, на которых программа встаёт в ступор и может прерывать работу. Причем это бывает неоднократно и внезапно после нескольких запусков он может всё-таки откликнуться на эту вакансию. Причина неизвестна. Вариант решения: с отключенным режимом headless вручную откликнуться на эту вакансию и запустить программу по новой.
- **Поломка браузера**: на самых ранних версиях программы один единственный раз столкнулся с тем, что произошла рассинхронизация браузера Google Chrome с профилем гугла и простым релогом это не решалось, багнулось намертво, пришлось переустановить его два или три раза... Для тех, у кого включена синхронизация с профилем это не должно стать проблемой, так как после установки всё вернётся. А вот если вы держите настройки локально - найдите их и сделайте бэкап перед установкой.
