# dc-ctf
# Этап 1

Итак, для начала переходим по ссылке http://ctf.dc8044.com:8044/

Первым делом смотрим исходный код страницы (Ctrl + U)

Тут интереснее уже:

![](https://github.com/bondss/dc-ctf/blob/master/screenshots/task_1.png "Task 1")

# Этап 2

Теперь наша ссылка принимает следующий вид: http://ctf.dc8044.com:8044/dc8044kyiv/

Опять лезем в исходники:

![](https://github.com/bondss/dc-ctf/blob/master/screenshots/task_2.png "Task 2")

**Первая реакция:**

![](https://github.com/bondss/dc-ctf/blob/master/screenshots/Wat8.jpg "Wat")

Ну да ладно, тег ```<script>``` и конкретно ```console.log``` намекает на связь с JavaScript 

Пару минут в поисковиках и внезапно:

![](https://github.com/bondss/dc-ctf/blob/master/screenshots/task_2_1.png "Task2_1")

Я уверен, что гуру JS справились с этим быстрее, чем я.

# Этап 3

Опускаемся глубже: http://ctf.dc8044.com:8044/dc8044kyiv/111111111111111110000/

И... нас кидает обратно на главную.

![](https://github.com/bondss/dc-ctf/blob/master/screenshots/wtf.png "wtf")

Кажется, пора поиграться с прокси (или хотя бы с аддонами HTTP Headers в различных браузерах, их тысячи)

Составлем запрос вида: 

```
GET /dc8044kyiv/111111111111111110000/ HTTP/1.1
Host: ctf.dc8044.com:8044
````
Получаем ответ про 301 Moved Permanently и кое что поинтересней:

![](https://github.com/bondss/dc-ctf/blob/master/screenshots/task_3.png "Task 3")

# Этап 4

Открываем картинку: http://ctf.dc8044.com:8044/dc8044kyiv/111111111111111110000/lol_kek_cheburek.png

Сбивает с толку, что директории создавались на одном уровне. Но любопытство взяло верх (после кучи идиотских вариантов до этого) и в конце концов ссылка приобрела вид: http://ctf.dc8044.com:8044/dc8044kyiv/111111111111111110000/n33dm0r3/

# Этап 5 

Ок, исходники:

![](https://github.com/bondss/dc-ctf/blob/master/screenshots/task_4.png "Task 4")

Ага, настало время побрутить хэши.

[Hashcat docs](https://hashcat.net/wiki/doku.php?id=hybrid_attack)

Документация hashcat-а нам говорит, что можно использовать готовый шаблон (наш IP) в комбинации с вордлистом.

Ок, поехали (пример):

```
hashcat -a 7 HASH 127.0.0.1 example.dict
``` 
Под рукой был rockyou.txt, с ним и вскрылась вторая часть фразы (**password**).

# Финал

Итак, мы уже на самом дне, вскрываем последний слой:
http://ctf.dc8044.com:8044/dc8044kyiv/111111111111111110000/n33dm0r3/password/

И получаем ответ:

![](https://github.com/bondss/dc-ctf/blob/master/screenshots/task_5.png "Finality")

Вот и всё, спасибо организаторам за нескучную пятницу :)

**Have fun, try harder, never give up.**
