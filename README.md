# ØMQ - The Guide
# РУКОВОДСТВО

### Pieter Hintjens главный исполнительный директор iMatix.
Для всех комментариев и ошибок, пожалуйста используйте [трекер](https://github.com/imatix/zguide/issues). Данная версия руководства написана по последней стабильной версии ZeroMQ (3.2).
Если вы используете старую версию ZeroMQ то некоторые данные могуть различаться.
Руководство предоставляет примеры на Си, но так же PHP, Python, Lua, and Haxe. Так же мы перевели большинство примеров на C++, C#, CL, Delphi, Erlang, F#, Felix, Haskell, Java, Objective-C, Ruby, Ada, Basic, Clojure, Go, Haxe, Node.js, ooc, Perl, and Scala.


## Предисловие

### Кратко о ZeroMQ

ZeroMQ, так же известная как  ØMQ, 0MQ, zmq, или Зера, является встраиваемой сетевой библиотекой, но чаще всего  используется как мультипоточный фреймворк. Она предоставляет сокеты для передачи атомарных сообщений поверх различных транспортных уровней, таких как межпроцессное взаимодействие(IPC), TCP и широковещательная рассылка (multicast). Вы можете подключить сокеты М-М(многие ко многим) используя паттерны такие как  fan-out(сообщение передается во все прицепленные к ней очереди), pub-sub(издатель-подписчик), task distribution(распределение задач), и request-reply(запрос-ответ).Скорости Зеры достаточно, чтобы построить высоконагруженные кластеры. Асинхронная модель ввода/вывода развязывает руки для построения многопоточных приложений и распределенных задачи. Поддерживает множество языков программирования и запускается на большинстве популярных операционных системах. ZeroMQ от [iMatix](http://www.imatix.com/) распространяется под лицензией LGPLv3 с открытым исходным кодом.

### Как все начиналось (How It Began)

Мы взяли обычные tcp сокеты, добавили в них смесь радиоактивных изотопов похищенных из секретного советского проекта атомных исследований, бомбанули по нему космическими лучами 1950-х годов и отдали его в руки обдолбанного автора комиксов с фетишем обтягивающего трико. Да сокеты ZeroMQ это супергерои призванные спасти сетевой мир.

###### Рисунок 1: Страшная катастрофа.
![](https://github.com/imatix/zguide/raw/master/images/fig1.png)

### Дзен ZeroMQ (The Zen of Zero)

Ноль в наименовании ZeroMQ означает компромисс. С одной стороны такое странное название снижает позиции в поисковиках. С другой стороны это не хило бесит некоторых датчан, которые пишут нам такие вещи как "ØMG røtfl", и «Rødgrød med fløde!», что, по-видимому, является оскорблением, означающим - «пусть ваши соседи станут прямыми потомками Гренделя!» (прим. Грендель - чудовище из сказки про Беовульфа, которое пожирало соседствующих с ним датчан). Вроде бы справедливый обмен.

На самом деле ноль в наименовании ZeroMQ означает "нулевой брокер" и (как можно быстрее) "нулевая задержка". С того времени это привело к зарождению новой терминологии: Нулевое администрирование, нулевая стоимость, ноль отходов. В более общем плане «ноль» относится к культуре минимализма, концепции которой придерживается проект. Мы подкрутили мощность, удаляя сложность, а не функционал.

### Для кого эта книга (Audience)

Эта книга написана для профессиональных программистов, которые хотят узнать как создавать огромные распределенные системы доминирующие по производительности. Надеемся вы знаете и умеете читать код на Си, так как большинство примеров в книге приведены на Си, хотя ZeroMQ может быть применен во множестве языков. Предполагается что вам нужен лучший результат за меньшие деньги, иначе вы разочаруетесь компромиссами предоставленными ZeroMQ. Помимо базовых вещей, мы попытаемся представить все концепции сетевых и распределенных вычислений, они вам понадобятся при работе с ZeroMQ.

### Благодарности. (Acknowledgements)

Спасибо Andy Oram за возможность выхода книги [O'Reilly](http://shop.oreilly.com/product/0636920026136.do) и редактирования этого текста.

Спасибо Bill Desmarais, Brian Dorsey, Daniel Lin, Eric Desgranges, Gonzalo Diethelm, Guido Goldstein, Hunter Ford, Kamil Shakirov, Martin Sustrik, Mike Castleman, Naveen Chawla, Nicola Peduzzi, Oliver Smith, Olivier Chamoux, Peter Alexander, Pierre Rouleau, Randy Dryburgh, John Unwin, Alex Thomas, Mihail Minkov, Jeremy Avnet, Michael Compton, Kamil Kisiel, Mark Kharitonov, Guillaume Aubert, Ian Barber, Mike Sheridan, Faruk Akgul, Oleg Sidorov, Lev Givon, Allister MacLeod, Alexander D'Archangel, Andreas Hoelzlwimmer, Han Holl, Robert G. Jakabosky, Felipe Cruz, Marcus McCurdy, Mikhail Kulemin, Dr. Gergő Érdi, Pavel Zhukov, Alexander Else, Giovanni Ruggiero, Rick "Technoweenie", Daniel Lundin, Dave Hoover, Simon Jefford, Benjamin Peterson, Justin Case, Devon Weller, Richard Smith, Alexander Morland, Wadim Grasza, Michael Jakl, Uwe Dauernheim, Sebastian Nowicki, Simone Deponti, Aaron Raddon, Dan Colish, Markus Schirp, Benoit Larroque, Jonathan Palardy, Isaiah Peng, Arkadiusz Orzechowski, Umut Aydin, Matthew Horsfall, Jeremy W. Sherman, Eric Pugh, Tyler Sellon, John E. Vincent, Pavel Mitin, Min RK, Igor Wiedler, Olof Åkesson, Patrick Lucas, Heow Goodman, Senthil Palanisami, John Gallagher, Tomas Roos, Stephen McQuay, Erik Allik, Arnaud Cogoluègnes, Rob Gagnon, Dan Williams, Edward Smith, James Tucker, Kristian Kristensen, Vadim Shalts, Martin Trojer, Tom van Leeuwen, Hiten Pandya, Harm Aarts, Marc Harter, Iskren Ivov Chernev, Jay Han, Sonia Hamilton, Nathan Stocks, Naveen Palli, и Zed Shaw за их участие в этой работе.



## ГЛАВА 1 - ОСНОВЫ

### Исправление мира (Fixing the World)

Как можно описать ZeroMQ? Некоторые из нас начинают перечислять все плюшки которые предоставляет Зера. Это как сокеты на стероидах. Это как почтовые ящики с маршрутизацией. Это быстро! Другие попытаются поделиться своим моментом просветления, что по началу было сложно изменить в голове устоявшееся понимание сокетов, но однажды приходит понимание того, что обычные сокеты и сокеты зеры не одно и тоже. Все становится проще. Сложность уходит. Разум просветляется. Кто-то попытается объяснить на примере сравнения. Это проще, легковеснее, но все еще нам знакомо.

Программирование это наука завуалированная под искусство, так как большинство из нас не понимает программирования на физическом уровне и вообще редко когда изучает этот аспект. Физика программного обеспечения это не алгоритмы, структуры данных, языки и абстракции. Это просто инструменты, которые мы делаем, используем, а затем выбрасываем. Реальная физика ПО это физика человека - в частности наши физические ограничения, когда дело касается сложности ПО, а также наше решение работать в команде, чтобы разделить сложную реализацию на более мелкие кусочки. Наука программирования состоит в том, чтобы создать конструктивные блоки, легкие в понимании и использовании людьми, тогда и только тогда люди смогут решать казалось бы неподъемные задачи..

Мы живем в общающемся мире, когда все между собой контактирует и современное программное обеспечение должно подстраиваться под этот мир. Создание тяжеловесных решений с заделом  на будущее расширение, порождает многопоточный, очень связный код. Это больше не соответствует заповеди "чистого кода". Код должен взаимодействовать с кодом. Код должен быть говорящим, дружелюбным и легко подключаемым. Код должен стартовать как человеческий мозг, триллионами нейронных нитей с сообщениями в каждой из них, с громадной параллельной сетью, не имеющей центра управления, не имеющей точки отказа, но способный решать чрезвычайно сложные задачи. И это не случайно, что будущее программного кода выглядит как человеческий мозг, поскольку конечными точками каждой сети, на некотором уровне, являются человеческий мозг.

Поработайте с потоками, протоколами, или сетями и вы поймете что это практически невозможно. Это мечта. Даже соединение всего нескольких программ через несколько сокетов, на деле довольно неприятное занятие. Триллионы? Цена за такое даже невообразима. Связать компьютеры настолько сложно, что это породило много миллиардные бизнесы, по созданию сетевого программного обеспечения.

По-этому мы живем в мире где железо намного опережает наши способности его обуздать. Во время кризиса 80х годов, когда даже такие тимлиды как Фред Брукс не верили в существование "[серебряной пули](https://en.wikipedia.org/wiki/No_Silver_Bullet)", способной поднять планку хотя бы на единицу в производительности, надежности и простоте.

Брукс упустил из виду открытое ПО, помогающее справится с этим кризисом, подталкивающее нас более эффективно делиться опытом. Сегодня нас настиг другой кризис ПО, но мы про это промолчим. Только большие, богатые фирмы могут позволить себе разработку общающихся приложений. Существует облако, но оно закрытое. Наши персональные данные перекочевывают в облака, к которым у нас нет доступа и которым мы не конкуренты. Кто владеет нашими соцсетям? Это смахивает на революцию мейнфреймов в обратном направлении.

Ладно, оставим политическую философию для [другой книги](https://legacy.gitbook.com/book/hintjens/culture-empire/details). Дело в том, что хоть интернет и предполагает большой потенциал массового общающегося кода, реальность такова, что для большинства такая задача непреодолима, и большие интересные задачи (в здравоохранении, образовании, экономике, транспорте и тд.) остаются не решенными, так как нет возможности это все связать воедино, нет возможности продумать и работать совместно над этими проблемами.

Было множество попыток решения проблем общения между кодом. Существуют тысячи спецификаций IETF, каждая из которых разрешает часть головоломки. Для разработчиков приложений, HTTP - это пожалуй одно из простейших решений для работы, но порождающее проблему куда хуже - поощрение разработчиков и архитекторов думать большими сервисами и тонкими тупыми клиентами.

Сегодня все еще соединяют приложения посредством чистых UDP и TCP, закрытых протоколов, HTTP и веб-сокетов. Это порождает головную боль для разработчиков, медлительность, сложность в масштабировании, в также централизацию (точку отказа). Распределенные архитектуры P2P в основном предназначены для баловства, а не для работы. Сколько приложений использует Skype или Bittorrent для обмена данными?

Давайте задумаемся, чего же все такие не хватает. Чтобы исправить мир, нам нужно две вещи. Первая, решить проблему того, чтобы любой код мог взаимодействовать с любым кодом. Вторая, упаковать это в такой инструмент, который помогал бы легко конструировать блоки кода, простые для понимания и использования.

Звучит до смешного просто. Может так оно и есть. И в этом весь смысл.

## Соглашения (Starting Assumptions)

Договоримся, что вы используете версию Зеры не ниже 3.2. Договоримся, что все приведенные примеры приводятся для unix подобных операционных систем. Полагается, что вы умеете читать код на Си, чтобы более или менее понимать примеры. Договоримся, что под упоминанием обобщенных констант PUSH или SUBSCRIBE, имеются в виду ZMQ_PUSH или ZMQ_SUBSCRIBE, что зависит от языка программирования и вы сами подставите их в свой код.

### Примеры (Getting the Examples)

Примеры находятся в публичном [git репозитории](https://github.com/imatix/zguide). Простейшим путем будет просто клонировать их к себе в директорию.

`git clone --depth=1 git://github.com/imatix/zguide.git`

Далее в своей директории вы найдете примеры для различных языков программирования. Если все же ваш язык отсутствует, то мы поощряем предоставление примеров для него. Таким образом и появились все эти примеры, спасибо всем за приложенные к этому усилия. Все примеры распространяются по лицензии MIT/X11.

### Спроси и тебе ответят (Ask and Ye Shall Receive)

Давайте же уже перейдем к коду. Разумеется мы начнем с Hello World. Для начала создадим клиента и сервер. Клиент отправляет "HELLO" на сервер и получает в ответ "WORLD" (рис 2).

###### * Рисунок 2. Запрос-ответ (Request-Reply)*
![](https://github.com/imatix/zguide/raw/master/images/fig2.png)

В примере блок кода сервера на языке Си. Он открывает сокет Зеры на порту 5555, читает из него запросы и отвечает "WORLD" на каждый из них.

*сервер Hello World на СИ*

```C
//  Hello World server

#include <zmq.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <assert.h>

int main (void)
{
    //  Socket to talk to clients
    void *context = zmq_ctx_new ();
    void *responder = zmq_socket (context, ZMQ_REP);
    int rc = zmq_bind (responder, "tcp://*:5555");
    assert (rc == 0);

    while (1) {
        char buffer [10];
        zmq_recv (responder, buffer, 10, 0);
        printf ("Received Hello\n");
        sleep (1);          //  Do some 'work'
        zmq_send (responder, "World", 5, 0);
    }
    return 0;
}
```


Пара сокетов типа REQ-REP(запрос-ответ) являются последовательно-зависимой. Клиент в цикле сначала отправляет запрос [zmq_send()](http://api.zeromq.org/3-2:zmq_send) и только после этого ждет ответ [zmq_recv()](http://api.zeromq.org/3-2:zmq_recv). Использование другой последовательности (к примеру отправка подряд двух сообщений), приведет к тому, что функция вернет -1. Аналогичным образом сервисы сначала слушают запрос [zmq_recv()](http://api.zeromq.org/3-2:zmq_recv) и только после этого отправляют на него ответ [zmq_send()](http://api.zeromq.org/3-2:zmq_send).

Зера использует Си и это так же основной язык для написания примеров. Если вы читаете это на сайте, то внизу будут ссылки для примеров переведенных на разные языки. Теперь давайте сравним аналогичный сервер на С++:

###### *hwserver.cpp: Hello World server*
```C
//
//  Hello World server in C++
//  Binds REP socket to tcp://*:5555
//  Expects "Hello" from client, replies with "World"
//
#include <zmq.hpp>
#include <string>
#include <iostream>
#ifndef _WIN32
#include <unistd.h>
#else
#include <windows.h>

#define sleep(n)    Sleep(n)
#endif

int main () {
    //  Prepare our context and socket
    zmq::context_t context (1);
    zmq::socket_t socket (context, ZMQ_REP);
    socket.bind ("tcp://*:5555");

    while (true) {
        zmq::message_t request;

        //  Wait for next request from client
        socket.recv (&request);
        std::cout << "Received Hello" << std::endl;

        //  Do some 'work'
        sleep(1);

        //  Send reply back to client
        zmq::message_t reply (5);
        memcpy (reply.data (), "World", 5);
        socket.send (reply);
    }
    return 0;
}
```

Как вы можете убедиться, API для языков СИ и С++ аналогичны. На языке таком как php или java, мы можем скрыть большинство реализации и сделать код еще более легким и читаемым:

###### Пример 3. сервер Hello World на php (hwserver.php)

```php
<?php

/*
 *  Hello World server
 *  Binds REP socket to tcp://*:5555
 *  Expects "Hello" from client, replies with "World"
 *  @author Ian Barber <ian(dot)barber(at)gmail(dot)com>
 */

$context = new ZMQContext(1);

//  Socket to talk to clients
$responder = new ZMQSocket($context, ZMQ::SOCKET_REP);
$responder->bind("tcp://*:5555");

while (true) {
    //  Wait for next request from client
    $request = $responder->recv();
    printf ("Received request: [%s]\n", $request);

    //  Do some 'work'
    sleep (1);

    //  Send reply back to client
    $responder->send("World");
}
```

###### Пример сервера на других языках:
[ C++ ](http://zguide.zeromq.org/cpp:hwserver)|[ C# ](http://zguide.zeromq.org/cs:hwserver)|[ Clojure ](http://zguide.zeromq.org/clj:hwserver)|[ CL ](http://zguide.zeromq.org/lisp:hwserver)|[ Delphi ](http://zguide.zeromq.org/dpr:hwserver)|[ Erlang ](http://zguide.zeromq.org/es:hwserver)|[ F# ](http://zguide.zeromq.org/fsx:hwserver)|[ Felix ](http://zguide.zeromq.org/flx:hwserver)|[ Go ](http://zguide.zeromq.org/go:hwserver)|[ Haskell ](http://zguide.zeromq.org/hs:hwserver)|[ Haxe ](http://zguide.zeromq.org/hx:hwserver)|[ Lua ](http://zguide.zeromq.org/lua:hwserver)|[ Node.js ](http://zguide.zeromq.org/js:hwserver)|[ Objective-C ](http://zguide.zeromq.org/m:hwserver)|[ Perl ](http://zguide.zeromq.org/pl:hwserver)|[ PHP ](http://zguide.zeromq.org/php:hwserver)|[ Python ](http://zguide.zeromq.org/py:hwserver)|[ Q ](http://zguide.zeromq.org/q:hwserver)|[ Racket ](http://zguide.zeromq.org/rkt:hwserver)|[ Ruby ](http://zguide.zeromq.org/rb:hwserver)|[ Scala ](http://zguide.zeromq.org/scala:hwserver)|[ Tcl ](http://zguide.zeromq.org/tcl:hwserver)|[ Ada | Basic | Java | ooc ](http://zguide.zeromq.org/main:translate)

###### Пример клиента на других языках:
[ C++ ](http://zguide.zeromq.org/cpp:hwclient)|[ C# ](http://zguide.zeromq.org/cs:hwclient)|[ Clojure ](http://zguide.zeromq.org/clj:hwclient)|[ CL ](http://zguide.zeromq.org/lisp:hwclient)|[ Delphi ](http://zguide.zeromq.org/dpr:hwclient)|[ Erlang ](http://zguide.zeromq.org/es:hwclient)|[ F# ](http://zguide.zeromq.org/fsx:hwclient)|[ Felix ](http://zguide.zeromq.org/flx:hwclient)|[ Go ](http://zguide.zeromq.org/go:hwclient)|[ Haskell ](http://zguide.zeromq.org/hs:hwclient)|[ Haxe ](http://zguide.zeromq.org/hx:hwclient)|[ Lua ](http://zguide.zeromq.org/lua:hwclient)|[ Node.js ](http://zguide.zeromq.org/js:hwclient)|[ Objective-C ](http://zguide.zeromq.org/m:hwclient)|[ Perl ](http://zguide.zeromq.org/pl:hwclient)|[ PHP ](http://zguide.zeromq.org/php:hwclient)|[ Python ](http://zguide.zeromq.org/py:hwclient)|[ Q ](http://zguide.zeromq.org/q:hwclient)|[ Racket ](http://zguide.zeromq.org/rkt:hwclient)|[ Ruby ](http://zguide.zeromq.org/rb:hwclient)|[ Scala ](http://zguide.zeromq.org/scala:hwclient)|[ Tcl ](http://zguide.zeromq.org/tcl:hwclient)|[ Ada | Basic | Java | ooc ](http://zguide.zeromq.org/main:translate)

Теперь это выглядит слишком просто, чтобы быть правдой, но не забывайте, что сокеты Зеры имеют суперсилы. Вы можете навешать на этот сервер тысячи клиентов и он продолжит быстро и припеваючи работать. Ради интереса запустите сначала клиента и только потом сервер. Смотрите, это все еще работает и не падает, задумайтесь на секунду почему так происходит.

Давайте кратко посмотрим как эти две программы действительно работают. Они создают контекст Зеры и сокеты для работы. Не задумывайтесь о значении этих терминов. Скоро вы все поймете. Сервер навешивает свой сокет REP(ответ) на порт 5555. Сервер в цикле ожидает запроса, и отвечает на каждый. Клиент отправляет запрос и ожидает на него ответа. Если вы перезапустите сервер, клиент сам не поднимется. Поднятие после сбоят так просто не пройдет. Создание отказоустойчивых соединений типа запрос-ответ(request-reply),  довольно сложный процесс и мы до него еще дойдем, когда будем рассматривать в четвертой главе "надежные паттерны ответ-запрос" ("Reliable Request-Reply Patterns").

Многое происходит под капотом, но для нас программистов важно чтобы код был красивым, аккуратным и не падал под нагрузками. Паттерн запрос-ответ(request-reply), возможно простейший способ использования Зеры. Это отражение RPC и классической клиент-серверной модели.

### Сносочка про строки (A Minor Note on Strings)

Зера ничего не знает о том, что за данные вы отправляете, за исключением размера в байтах. Это означает что вся ответственность за форматирование и безопасность целиком на вас. Для отправки объектов и структур данных используйте специализированные библиотеки такие как Protocol Buffers. Но так же не забывайте позаботиться и о простых строковых данных.
В СИ и некоторых других языках строки оканчиваются нулевым байтом. Мы должны отправить строку типа "HELLO" вместе с закрывающим нулевым байтом.

```C
zmq_send (requester, "Hello", 6, 0);
```

Однако если вы используете другой язык, то можно не заботиться о нулевом байте. К примеру отправка той же строки на языке Python, выглядит вот так:

```Python
socket.send ("Hello")
```

Тогда, то, что будет отправлено это длинна(один байт определяющий длину) и содержимое строки в виде отдельных ее символов (рис 3).

###### *Рисунок 3. Строка Зеры.*

![Рисунок 3](https://github.com/imatix/zguide/raw/master/images/fig3.png)

И если вы читаете это на стороне кода Си, вы получите нечто выглядящее как строка (если повезет все пять байт выстроятся как надо), но ею не являющейся. Когда ваши клиент-серверные приложения не имеют согласованного формата строк, вы будете получать странные данные.

Когда вы получаете данные на стороне языка Си, нельзя безоговорочно доверять тому, что строка будет корректно завершена null байтом. Каждый раз при приеме сообщения вам нужно выделить память под эту строку с учетом закрывающего байта, скопировать туда строку и самостоятельно завершить строку null байтом. В таком случае давайте установим правило - Строки Зеры зависимы от длинны и не имеют закрывающего null байта. В лучшем случае Зера обработает кусок сообщения, как показано на рисунке выше - с учетом байта длины и последующих за ним байт.

Вот что необходимо сделать на стороне кода на Си чтобы получить строку и корректно ее обработать для превращения в корректную строку.


```C
// Receive 0MQ string from socket and convert into C string
// Chops string at 255 chars, if it's longer
static char *
s_recv (void *socket) {
 	char buffer [256];
 	int size = zmq_recv (socket, buffer, 255, 0);
 	if (size == -1)
 	return NULL;
 	if (size > 255)
 	size = 255;
 	buffer [size] = 0;
 	return strdup (buffer);
}
```

Этот код можно превратить во вспомогательную функцию и подключать ее в заголовках. Собственно что и сделано в  zhelpers.h. Это поможет сделать разработку на Зере красивее и приятнее на языке СИ. Код слишком длинный, чтобы его тут выплевывать, так что истинные фанатики СИ прочтут его на досуге(https://github.com/booksbyus/zguide/blob/master/examples/C/zhelpers.h).

### Проверка версии (Version Reporting)

Зера существует в нескольких версиях и если вы столкнулись с какой-то проблемой, то скорее всего это уже исправлено в новой версии. Так что полезно знать какую версию либы вы используете. Вот маленькая программа позволяющая определить текущую версию.

###### Пример 5. Проверка версии ØMQ (version.c)
```c
// Report 0MQ version

#include <zmq.h>

int main (void)
{
	int major, minor, patch;
	zmq_version (&major, &minor, &patch);
	printf ("Current 0MQ version is %d.%d.%d\n", major, minor, patch);
    return 0;
}

```

[C++](http://zguide.zeromq.org/cpp:version) | [C#](http://zguide.zeromq.org/cs:version) | [Clojure](http://zguide.zeromq.org/clj:version) | [CL](http://zguide.zeromq.org/lisp:version) | [Delphi](http://zguide.zeromq.org/dpr:version) | [Erlang](http://zguide.zeromq.org/es:version) | [F#](http://zguide.zeromq.org/fsx:version) | [Felix](http://zguide.zeromq.org/flx:version) | [Go](http://zguide.zeromq.org/go:version) | [Haskell](http://zguide.zeromq.org/hs:version) | [Java](http://zguide.zeromq.org/java:Version) | [Lua](http://zguide.zeromq.org/lua:version) | [Node.js](http://zguide.zeromq.org/js:version) | [Objective-C](http://zguide.zeromq.org/m:version) | [Perl](http://zguide.zeromq.org/pl:version) | [PHP](http://) | [Python](http://zguide.zeromq.org/py:version) | [Q](http://zguide.zeromq.org/q:version) | [Ruby](http://zguide.zeromq.org/rb:version) | [Scala](http://zguide.zeromq.org/scala:version) | [Tcl](http://zguide.zeromq.org/tcl:version) | [Ada](http://zguide.zeromq.org/main:translate) | [Basic](http://zguide.zeromq.org/main:translate) | [Haxe](http://zguide.zeromq.org/main:translate) | [ooc](http://zguide.zeromq.org/main:translate/) | [Racket](http://zguide.zeromq.org/main:translate)


### Получение сообщения (Getting the Message Out)

Второй классический паттерн это односторонняя пересылка, когда сервер отправляет обновления набору клиентов. Давайте посмотрим на пример, в котором сервер отправляет обновления почтовых индексов, температуры и влажности. Будем генерировать произвольные значения, чтобы эмулировать поведения погоды.

Пример сервера. Используем порт 5556 для приложения.

###### Пример 6. Погодный сервер на Си (wuserver.c)

```C
//  Weather update server
//  Binds PUB socket to tcp://*:5556
//  Publishes random weather updates

#include "zhelpers.h"

int main (void)
{
    //  Prepare our context and publisher
    void *context = zmq_ctx_new ();
    void *publisher = zmq_socket (context, ZMQ_PUB);
    int rc = zmq_bind (publisher, "tcp://*:5556");
    assert (rc == 0);

    //  Initialize random number generator
    srandom ((unsigned) time (NULL));
    while (1) {
        //  Get values that will fool the boss
        int zipcode, temperature, relhumidity;
        zipcode     = randof (100000);
        temperature = randof (215) - 80;
        relhumidity = randof (50) + 10;

        //  Send message to all subscribers
        char update [20];
        sprintf (update, "%05d %d %d", zipcode, temperature, relhumidity);
        s_send (publisher, update);
    }
    zmq_close (publisher);
    zmq_ctx_destroy (context);
    return 0;
}

```
[C++](http://zguide.zeromq.org/cpp:wuserver) | [C#](http://zguide.zeromq.org/cs:wuserver) | [Clojure](http://zguide.zeromq.org/clj:wuserver) | [CL](http://zguide.zeromq.org/lisp:wuserver) | [Delphi](http://zguide.zeromq.org/dpr:wuserver) | [Erlang](http://zguide.zeromq.org/es:wuserver) | [F#](http://zguide.zeromq.org/fsx:wuserver) | [Felix](http://zguide.zeromq.org/flx:wuserver) | [Go](http://zguide.zeromq.org/go:wuserver) | [Haskell](http://zguide.zeromq.org/hs:wuserver) | [Haxe](http://zguide.zeromq.org/hx:wuserver) | [Java](http://zguide.zeromq.org/java:Wuserver) | [Lua](http://zguide.zeromq.org/lua:wuserver) | [Node.js](http://zguide.zeromq.org/js:wuserver) | [Objective-C](http://zguide.zeromq.org/m:wuserver) | [Perl](http://zguide.zeromq.org/pl:wuserver) | [PHP](http://zguide.zeromq.org/php:wuserver) | [Python](http://zguide.zeromq.org/py:wuserver) | [Racket](http://zguide.zeromq.org/rkt:wuserver) | [Ruby](http://zguide.zeromq.org/rb:wuserver) | [Scala](http://zguide.zeromq.org/scala:wuserver) | [Tcl](http://zguide.zeromq.org/tcl:wuserver) | [Ada](http://zguide.zeromq.org/main:translate) | [Basic](http://zguide.zeromq.org/main:translate) | [ooc](http://zguide.zeromq.org/main:translate) | [Q](http://zguide.zeromq.org/main:translate)

Это нескончаемый широковещательный поток (рис.4)

###### Рисунок 4.
![](https://github.com/imatix/zguide/raw/master/images/fig4.png)

Пример клиента который слушает все оповещения об изменениях и парсит их. По дефолту почтовый индекс будет для Нью Йорка.

###### Пример 7. Клиент погодного сервера (wuclient.c)

```C
//  Weather update client
//  Connects SUB socket to tcp://localhost:5556
//  Collects weather updates and finds avg temp in zipcode

#include "zhelpers.h"

int main (int argc, char *argv [])
{
    //  Socket to talk to server
    printf ("Collecting updates from weather server…\n");
    void *context = zmq_ctx_new ();
    void *subscriber = zmq_socket (context, ZMQ_SUB);
    int rc = zmq_connect (subscriber, "tcp://localhost:5556");
    assert (rc == 0);

    //  Subscribe to zipcode, default is NYC, 10001
    char *filter = (argc > 1)? argv [1]: "10001 ";
    rc = zmq_setsockopt (subscriber, ZMQ_SUBSCRIBE,
                         filter, strlen (filter));
    assert (rc == 0);

    //  Process 100 updates
    int update_nbr;
    long total_temp = 0;
    for (update_nbr = 0; update_nbr < 100; update_nbr++) {
        char *string = s_recv (subscriber);

        int zipcode, temperature, relhumidity;
        sscanf (string, "%d %d %d",
            &zipcode, &temperature, &relhumidity);
        total_temp += temperature;
        free (string);
    }
    printf ("Average temperature for zipcode '%s' was %dF\n",
        filter, (int) (total_temp / update_nbr));

    zmq_close (subscriber);
    zmq_ctx_destroy (context);
    return 0;
}
```

[C++](http://zguide.zeromq.org/cpp:wuclient) | [C#](http://zguide.zeromq.org/cs:wuclient) | [Clojure](http://zguide.zeromq.org/clj:wuclient) | [CL](http://zguide.zeromq.org/lisp:wuclient) | [Delphi](http://zguide.zeromq.org/dpr:wuclient) | [Erlang](http://zguide.zeromq.org/es:wuclient) | [F#](http://zguide.zeromq.org/fsx:wuclient) | [Felix](http://zguide.zeromq.org/flx:wuclient) | [Go](http://zguide.zeromq.org/go:wuclient) | [Haskell](http://zguide.zeromq.org/hs:wuclient) | [Haxe](http://zguide.zeromq.org/hx:wuclient) | [Java](http://zguide.zeromq.org/java:Wuclient) | [Lua](http://zguide.zeromq.org/lua:wuclient) | [Node.js](http://zguide.zeromq.org/js:wuclient) | [Objective-C](http://zguide.zeromq.org/m:wuclient) | [Perl](http://zguide.zeromq.org/pl:wuclient) | [PHP](http://zguide.zeromq.org/php:wuclient) | [Python](http://zguide.zeromq.org/py:wuclient) | [Racket](http://zguide.zeromq.org/rkt:wuclient) | [Ruby](http://zguide.zeromq.org/rb:wuclient) | [Scala](http://zguide.zeromq.org/scala:wuclient) | [Tcl](http://zguide.zeromq.org/tcl:wuclient) | [Ada](http://zguide.zeromq.org/main:translate) | [Basic](http://zguide.zeromq.org/main:translate) | [ooc](http://zguide.zeromq.org/main:translate) | [Q](http://zguide.zeromq.org/main:translate)

Обратите внимание, что когда вы используете SUB сокет, вы ДОЛЖНЫ подписаться используя функцию [zmq_setsockopt()](http://api.zeromq.org/3-2:zmq_setsockopt) как это делалось в примере. Если вы ни на что не подписались, вы ничего не получите. Это распространенная ошибка новичков. Подписчик может одновременно подписаться на множество каналов. И если обновление соответствует любой из этих подписок то подписчик получит это сообщение. Также есть возможность отписаться от любой подписки. Подписка чаще всего задается в виде человекочитаемой стоки, но это не жесткое ограничение. Дополнительно можно посмотреть в описании функции [zmq_setsockopt()](http://api.zeromq.org/3-2:zmq_setsockopt).

Пара сокетов издатель-подписчик(PUB-SUB) является асинхронной. Клиент в цикле или единожды если нужно, вызывает [zmq_recv()](http://api.zeromq.org/3-2:zmq_recv). Попытка отправить сообщение по SUB сокету вызовет ошибку. Аналогично, сервис вызывает [zmq_send()](http://api.zeromq.org/3-2:zmq_send), когда есть что отправить, но не может вызвать [zmq_recv()](http://api.zeromq.org/3-2:zmq_recv) на сокете издателя(PUB).

Теоретически Зере плевать кто слушает, а кто подключается к сокету. Однако на практике есть недокументированные отличия, о которых мы поговорим позже. Сейчас просто привязываемся PUB и подключаемся к SUB.

Еще одна важная вещь с сокетами типа подписчик-издатель, которую нужно знать и учитывать. Вы не знаете когда подписчик начнет получить сообщения. Даже если вы сначала запустите подписчика и только после этого, выдержав паузу, запустите издателя, ПОДПИСЧИК ВСЕГДА ПРОПУСТИТ ПЕРВОЕ СООБЩЕНИЕ. Это случается потому что пока подписчик подключается(обычно это делается быстро, но не моментально), издатель уже может отправить сообщение. Поскольку множество людей натыкаются на этот казус, давайте остановимся на нем подробнее. Запомните, что Зера выполняет асинхронное чтение и отправку в фоновом режиме. Предположим у нас есть два узла которые выполняются в следующем порядке.


* Подписчик подключается к конечной точке, получает сообщения и считает сколько он получил сообщений.
* Издатель привязывается к конечной точке и немедленно отправляет 1000 сообщений.

В таком случае, подписчик скорее всего ничего не получит. Вы в замешательстве, проверяете, что правильно указали параметры подключения, пробуете снова и опять ничего не получили. Создание TCP соединения требует подтверждения связи между конечными узлами, что требует какое-то время, которое зависит от вашей сети  и количества хопов между конечными точками. За это время Зера уже отправит кучу сообщений. К примеру для установки канала требуется 5 мс и этот же канал способен обрабатывать миллион сообщений в секунду. Когда подписчику требуется целых 5 мс на установку соединения, издателю потребуется всего 1 мс на отправку всей тысячи сообщений.

В [главе 2 - "Паттерны по сокетам"](http://) мы расскажем как синхронизировать издателя и подписчика, таким образом, чтобы сообщения не отправлялись пока все подписчики не подключатся и будут готовы получать сообщения. Существует простой и тупейший способ заставить издателя подождать - поставить ему задержку. Не стоит так делать, это тупейший, не красивый и медленный способ. Подождите до [главы 2 - "Паттерны по сокетам"](http://) и вы все узнаете.

Существует еще один способ. Принять решение что наш поток данных бесконечный и подписчику плевать на то, что приходило до его подключения. Как к примеру в нашем примере с погодными данными.

Клиент подписывается на рассылку почтовых индексов и собирает тысячу обновлений для почтовых индексов. Сервис может сгененировать 10 миллионов сообщений. Вы можете сначала запустить клиента, потом сервис, и клиент продолжить работать. Вы можете перезапускать сервис когда вам вздумается и клиент продолжит работать. Когда подписчик соберет 1000 сообщений, он их обработает, выведет и завершится.


Некоторые аспекты по паттерну подписчик-издатель(pub-sub):

* Подписчик может подписываться на множество издателей единовременно. Данные будут приходить поочередно(справедливая очередь), таким образом один издатель не глушит другого.

* Если на издателя никто не подписался, он просто будет отбрасывать все сообщения.

* Если вы используете TCP соединение и подписчик тормозит то сообщения будут накапливаться в очереди у издателя. Как защитить издателей от переполнения буфера в таких ситуациях, путем установки ограничения, рассмотрим позже.

* Начиная с Зеры версии 3 и выше, если вы используете протоколы tcp:// или ipc:// фильтрация происходит на стороне издателя. При использовании протокола epgm:// фильтрация происходит на стороне подписчика. В версиях со второй по третью вся фильтрация происходит на стороне подписчика.

Ниже показано сколько времени занимает получение и фильтрация 10 миллионов сообщений, на моем лэптопе с процессором intel i5 поколения 2011 года. Прилично, но ничего особенного.

```bash
$ time wuclient
Collecting updates from weather server...
Average temperature for zipcode '10001 ' was 28F
real 0m4.470s
user 0m0.000s
sys 0m0.008s
```

### Разделяй и властвуй (Divide and Conquer)

###### Рисунок 5. Параллельные пайпы

![](https://github.com/imatix/zguide/raw/master/images/fig5.png)

В качестве последнего примера (вы наверняка уже устали от кода и хотели бы вернуться к философствованию и обсуждению абстракций), давайте произведем немного суперкомпьютеров. Наше суперкомпьютерное приложение является довольно типичной моделью параллельной обработки.

У нас есть:
* Вентилятор, создающий задачи для параллельного выполнения.
* Набор воркеров, которые могут обрабатывать задачи.
* Сток(имеется ввиду место куда попадают все данные), способный собирать воедино данные от воркеров.

В действительности воркеры запускаются в быстродействующих контейнерах, может даже на графических процессорах для сложных расчетов. Вентилятор генерирует 100 задач, каждое из которых говорит воркеру спать определенное количество миллисекунд.

###### Пример 8. Вентелятор для параллельных задач (Parallel task ventilator) (taskvent.c)

```C
//  Task ventilator
//  Binds PUSH socket to tcp://localhost:5557
//  Sends batch of tasks to workers via that socket

#include "zhelpers.h"

int main (void)
{
    void *context = zmq_ctx_new ();

    //  Socket to send messages on
    void *sender = zmq_socket (context, ZMQ_PUSH);
    zmq_bind (sender, "tcp://*:5557");

    //  Socket to send start of batch message on
    void *sink = zmq_socket (context, ZMQ_PUSH);
    zmq_connect (sink, "tcp://localhost:5558");

    printf ("Press Enter when the workers are ready: ");
    getchar ();
    printf ("Sending tasks to workers…\n");

    //  The first message is "0" and signals start of batch
    s_send (sink, "0");

    //  Initialize random number generator
    srandom ((unsigned) time (NULL));

    //  Send 100 tasks
    int task_nbr;
    int total_msec = 0;     //  Total expected cost in msecs
    for (task_nbr = 0; task_nbr < 100; task_nbr++) {
        int workload;
        //  Random workload from 1 to 100msecs
        workload = randof (100) + 1;
        total_msec += workload;
        char string [10];
        sprintf (string, "%d", workload);
        s_send (sender, string);
    }
    printf ("Total expected cost: %d msec\n", total_msec);

    zmq_close (sink);
    zmq_close (sender);
    zmq_ctx_destroy (context);
    return 0;
}
```
[C++](http://zguide.zeromq.org/cpp:taskvent) | [C#](http://zguide.zeromq.org/cs:taskvent) | [Clojure](http://zguide.zeromq.org/clj:taskvent) | [CL](http://zguide.zeromq.org/lisp:taskvent) | [Delphi](http://zguide.zeromq.org/dpr:taskvent) | [Erlang](http://zguide.zeromq.org/es:taskvent) | [F#](http://zguide.zeromq.org/fsx:taskvent) | [Felix](http://zguide.zeromq.org/flx:taskvent) | [Go](http://zguide.zeromq.org/go:taskvent) | [Haskell](http://zguide.zeromq.org/hs:taskvent) | [Haxe](http://zguide.zeromq.org/hx:taskvent) | [Java](http://zguide.zeromq.org/java:Taskvent) | [Lua](http://zguide.zeromq.org/lua:taskvent) | [Node.js](http://zguide.zeromq.org/js:taskvent) | [Objective-C](http://zguide.zeromq.org/m:taskvent) | [Perl](http://zguide.zeromq.org/pl:taskvent) | [PHP](http://zguide.zeromq.org/php:taskvent) | [Python](http://zguide.zeromq.org/py:taskvent) | [Ruby](http://zguide.zeromq.org/rb:taskvent) | [Scala](http://zguide.zeromq.org/scala:taskvent) | [Tcl](http://zguide.zeromq.org/tcl:taskvent) | [Ada](http://zguide.zeromq.org/main:translate) | [Basic](http://zguide.zeromq.org/main:translate) | [ooc](http://zguide.zeromq.org/main:translate) | [Q](http://zguide.zeromq.org/main:translate) | [Racket](http://zguide.zeromq.org/main:translate)

А вот пример воркера. Он получает сообщение, спит определенное количество секунд, после чего сообщает, что он закончил.

###### Пример 9. Параллельний воркер (taskwork.c)

```C
//  Task worker
//  Connects PULL socket to tcp://localhost:5557
//  Collects workloads from ventilator via that socket
//  Connects PUSH socket to tcp://localhost:5558
//  Sends results to sink via that socket

#include "zhelpers.h"

int main (void)
{
    //  Socket to receive messages on
    void *context = zmq_ctx_new ();
    void *receiver = zmq_socket (context, ZMQ_PULL);
    zmq_connect (receiver, "tcp://localhost:5557");

    //  Socket to send messages to
    void *sender = zmq_socket (context, ZMQ_PUSH);
    zmq_connect (sender, "tcp://localhost:5558");

    //  Process tasks forever
    while (1) {
        char *string = s_recv (receiver);
        printf ("%s.", string);     //  Show progress
        fflush (stdout);
        s_sleep (atoi (string));    //  Do the work
        free (string);
        s_send (sender, "");        //  Send results to sink
    }
    zmq_close (receiver);
    zmq_close (sender);
    zmq_ctx_destroy (context);
    return 0;
}
```

[C++](http://zguide.zeromq.org/cpp:taskwork) | [C#](http://zguide.zeromq.org/cs:taskwork) | [Clojure](http://zguide.zeromq.org/clj:taskwork) | [CL](http://zguide.zeromq.org/lisp:taskwork) | [Delphi](http://zguide.zeromq.org/dpr:taskwork) | [Erlang](http://zguide.zeromq.org/es:taskwork) | [F#](http://zguide.zeromq.org/fsx:taskwork) | [Felix](http://zguide.zeromq.org/flx:taskwork) | [Go](http://zguide.zeromq.org/go:taskwork) | [Haskell](http://zguide.zeromq.org/hs:taskwork) | [Haxe](http://zguide.zeromq.org/hx:taskwork) | [Java](http://zguide.zeromq.org/java:Taskwork) | [Lua](http://zguide.zeromq.org/lua:taskwork) | [Node.js](http://zguide.zeromq.org/js:taskwork) | [Objective-C](http://zguide.zeromq.org/m:taskwork) | [Perl](http://zguide.zeromq.org/pl:taskwork) | [PHP](http://zguide.zeromq.org/php:taskwork) | [Python](http://zguide.zeromq.org/py:taskwork) | [Ruby](http://zguide.zeromq.org/rb:taskwork) | [Scala](http://zguide.zeromq.org/scala:taskwork) | [Tcl](http://zguide.zeromq.org/tcl:taskwork) | [Ada](http://zguide.zeromq.org/main:translate) | [Basic](http://zguide.zeromq.org/main:translate) | [ooc](http://zguide.zeromq.org/main:translate) | [Q](http://zguide.zeromq.org/main:translate) | [Racket](http://zguide.zeromq.org/main:translate)

А вот наше приложение для сбора результатов. Оно собирает данные от 100 задач и рассчитывается время их выполнения. Так мы сможем убедиться что задачи выполнялись параллельно, если воркеров было несколько.

###### Пример 10. Сток асинхронных результатов (tasksink.c)

```C
//  Task sink
//  Binds PULL socket to tcp://localhost:5558
//  Collects results from workers via that socket

#include "zhelpers.h"

int main (void)
{
    //  Prepare our context and socket
    void *context = zmq_ctx_new ();
    void *receiver = zmq_socket (context, ZMQ_PULL);
    zmq_bind (receiver, "tcp://*:5558");

    //  Wait for start of batch
    char *string = s_recv (receiver);
    free (string);

    //  Start our clock now
    int64_t start_time = s_clock ();

    //  Process 100 confirmations
    int task_nbr;
    for (task_nbr = 0; task_nbr < 100; task_nbr++) {
        char *string = s_recv (receiver);
        free (string);
        if ((task_nbr / 10) * 10 == task_nbr)
            printf (":");
        else
            printf (".");
        fflush (stdout);
    }
    //  Calculate and report duration of batch
    printf ("Total elapsed time: %d msec\n",
        (int) (s_clock () - start_time));

    zmq_close (receiver);
    zmq_ctx_destroy (context);
    return 0;
}

```
[C++](http://zguide.zeromq.org/cpp:tasksink) | [C#](http://zguide.zeromq.org/cs:tasksink) | [Clojure](http://zguide.zeromq.org/clj:tasksink) | [CL](http://zguide.zeromq.org/lisp:tasksink) | [Delphi](http://zguide.zeromq.org/dpr:tasksink) | [Erlang](http://zguide.zeromq.org/es:tasksink) | [F#](http://zguide.zeromq.org/fsx:tasksink) | [Felix](http://zguide.zeromq.org/flx:tasksink) | [Go](http://zguide.zeromq.org/go:tasksink) | [Haskell](http://zguide.zeromq.org/hs:tasksink) | [Haxe](http://zguide.zeromq.org/hx:tasksink) | [Java](http://zguide.zeromq.org/java:Tasksink) | [Lua](http://zguide.zeromq.org/lua:tasksink) | [Node.js](http://zguide.zeromq.org/js:tasksink) | [Objective-C](http://zguide.zeromq.org/m:tasksink) | [Perl](http://zguide.zeromq.org/pl:tasksink) | [PHP](http://zguide.zeromq.org/php:tasksink) | [Python](http://zguide.zeromq.org/py:tasksink) | [Ruby](http://zguide.zeromq.org/rb:tasksink) | [Scala](http://zguide.zeromq.org/scala:tasksink) | [Tcl](http://zguide.zeromq.org/tcl:tasksink) | [Ada](http://zguide.zeromq.org/main:translate) | [Basic](http://zguide.zeromq.org/main:translate) | [ooc](http://zguide.zeromq.org/main:translate) | [Q](http://zguide.zeromq.org/main:translate) | [Racket](http://zguide.zeromq.org/main:translate)

Среднее время выполнения 5 сек. Когда мы запустим 1,2 или 4 воркера мы получим результаты схожие с этими:

- 1 воркер:  Общее время выполнения 5034 мс
- 2 воркера: Общее время выполнения 2421 мс
- 4 воркера: Общее время выполнения 1018 мс

Давайте подробнее рассмотрим код.

* Воркеры читают данные из вентилятора и отправляют их в сток. Это означает что вы можете произвольно добавлять воркеров. Если бы конечные точки задавались на воркерах вам пришлось бы: Первое - использовать больше конечных точек и второе - постоянно перезапускать вентилятор и сток, как только вы добавили воркера. Поэтому мы решили, что вентилятор и сток будут статичными, а воркеры динамичными.

* Мы должны синхронизировать начало отправки со всеми подключившимися воркерами. Это довольно распространенная проблема встречающаяся в Зере и волшебной таблетки увы не существует. Метод zmq_connect занимает определенное время. Поэтому первый подключившийся воркер, успеет получить и обработать всю пачку задач пока все остальные подключаются. Если вы не синхронизируете запуск всей пачки сообщений, система не будет работать параллельно. Можете попробовать и убрать ожидание в вентиляторе.

* PUSH сокет вентилятора равномерно распределяет задачи между воркерами(при условии что они все подключились к моменту раздачи). Это называется "балансировкой нагрузки"(load-balancing). Это мы опять же рассмотрим позже.

* PULL сокет стока, равномерно собирает результаты от воркеров. Это называется "справедливой очередью" (fair-queuing) (см. рисунок 6).

###### Рисунок 6. Справедливая очередь (fair-queuing)

![](https://github.com/imatix/zguide/raw/master/images/fig6.png)

Конвейерному паттерну(pipeline pattern) также свойственен синдром "тормознутого присоединения"(slow joiner), что приводит к мысли, что PUSH сокет неправильно использует балансировщик нагрузки. Если вы используете пару PUSH/PULL и один из ваших воркеров получает больше задач чем остальные, это связано с тем, что PULL сокет вашего воркера быстрее подключается чем остальные, и хапает слишком много сообщений, пока другие не подключились. Если вы ищите способы правильной балансировки, то вам необходимо прочитать [Главу 3 - "Продвинутые паттерны запрос-ответ" (Advanced
Request-Reply Pattern).](http://)


### Программирование с зерой. (Programming with ØMQ)

Рассмотрев несколько примеров, вы скорее всего уже рветесь внедрять Зеру в свои проекты. Не спешите, сделайте глубокий вдох и задумайтесь над теми советами, которые сэкономят вам время и нервы.

* Шаг за шагом полностью изучите Зеру. Это не большой api, но он дает уйму возможностей.

* Пишите чистый код. Код с душком несет в себе кучу проблем и усложняет жизнь, как вам, так и тем кто будет работать после вас. Вы можете привыкнуть к несуразным названиям переменных, но людям, кто заглянет в ваш код, захочется вздернутся от такого кода. Используйте наименование отражающее реальность. Не надо думать, что вы слишком круты, чтобы объяснять посредством переменных, что происходит в коде. Пишите хороший код и всем будет легче.

* Пишите тесты. Это поможет вам разобраться с магией Зеры и понять, что ошибка кроется именно в этих вот пяти строках. Особенно это полезно на первых порах освоения Зеры.

* Если у вас что-то работает не так как вы ожидаете, разбейте ваш код на составные части и протестируйте каждый по отдельности

* Используйте абстракции(Классы, методы, без разницы). Не забывайте, что при копипасте кода, вы копируете и ошибки тоже.

### Получайте контекст правильно (Getting the Context Right)

Первым шагом при работе с Зерой, всегда будет создание контекста и использование его при создании сокетов. В Си это вызов метода [zmq_ctx_new()](http://api.zeromq.org/3-2:zmq_ctx_new). Можно использовать только один экземпляр контекста на процесс. Говоря техническим языком, контекст это контейнер для сокетов текущего процесса, и выполняет транспортную функцию для сокетов inproc, которые являются самыми быстрыми для передачи данных между процессами. Если процесс имеет два контекста, то они являются разными экземплярами Зеры. Используйте несколько экземпляров, если вам действительно это необходимо. Однако если нужды в этом нет, то запомните:

**Единажды вызывайте** [zmq_ctx_new()](http://api.zeromq.org/3-2:zmq_ctx_new) **в начале и единажды его удаляйте** [zmq_ctx_destroy()](http://api.zeromq.org/3-2:zmq_ctx_destroy) **в конце.**

Если вы форкаете свои процессы, то каждый из процессов потомков должен иметь свой отдельный контекст. Если вы вызывает [zmq_ctx_new()](http://api.zeromq.org/3-2:zmq_ctx_new) до форка, то можно не беспокоиться, каждый из потомков получит свой собственный контекст. В основном все интересные процессы протекают в процессах потомках, а родительский процесс просто ими управляет.

### Подчищайте за собой (Making a Clean Exit)

У классных программистов есть девиз - хорошие киллеры всегда подчищают за собой. Если вы использует языки подобные Python, то все подчистится автоматически. Но когда вы используете Си, необходимо внимательно относиться к уничтожению объектов когда они уже не нужны, иначе вы получите утечку памяти, нестабильное приложение и минус в карму.

Утечка памяти одно дело, другое дело в том, что Зера очень чувствительна к тому как вы завершаете свою программу. Если вы оставите открытыми сокеты, то функция [zmq_ctx_destroy()](http://api.zeromq.org/3-2:zmq_ctx_destroy) будет висеть вечно. Даже если вы закрываете сокеты, но имеются ожидающие подключения или отправки, то [zmq_ctx_destroy()](http://api.zeromq.org/3-2:zmq_ctx_destroy) будет ждать вечно, если вы не установить сокетам LINGER в ноль, перед их закрытием.

Объекты за которыми нам нужно следить это - сообщения, сокеты и контексты. К счастью это довольно легко делается, особенно в простых программах.

* По возможности Используйте [zmq_send()](http://api.zeromq.org/3-2:zmq_send) и  [zmq_recv()](http://api.zeromq.org/3-2:zmq_recv), это избавит от непосредственной работы с объектами zmq_msg_t.
* Если вы пользуететсь [zmq_recv()](http://api.zeromq.org/3-2:zmq_recv), то после получения сообщения, сразу вызывайте [zmq_msg_close()](http://api.zeromq.org/3-2:zmq_msg_close).
* Если у вас в обороте целая пачка сокетов, которые постоянно приходится открывать и закрывать, то это звоночек, что вам необходимо пересмотреть архитектуру своего приложения. В большинстве случает сокеты не закрываются до момента закрытия приложения.
* При завершении программы закройте сокеты и вызовите [zmq_ctx_destroy()](http://api.zeromq.org/3-2:zmq_ctx_destroy). Это закроет контекст.

Это все имеет значение, если вы программируете на Си подобном языке. На языках с авто сборщиком мусора, объекты подчистятся автоматически, как только вы закроете программу. Если вы используете исключения и операторные скобки, не забывайте подчищать за собой, к примеру в блоке "final".

А вот если ваше приложение многопоточное, то тут все становится куда сложнее. В следующей главе мы подробно поговорим про многопоточность. Но поскольку многие из вас пытаются бегать до того как научились ходить, то ниже мы, на скорую руку, накидаем коротенькое руководство о том, как завершать многопоточные приложения.

Ну во-первых не используйте один и тот же сокет из разных потоков. Пожалуйста не спорьте об этом, а просто не делайте так и все. После этого нужно отключить все сокеты имеющие запросы. Верным действием будет установить ожидание(LINGER) равным 1 секунде, после чего закрыть сокет.

Ну и наконец уничтожьте контекст. Это приведет к тому что все отправки, получения или накопители дочерних процессов вывалятся с исключениями. Отловите их, установите задержку, и позакрывайте сокеты этих потоков, после чего можно завершить потоки. Не уничтожайте контексты дважды. И не забывайте что [zmq_ctx_destroy](http://api.zeromq.org/3-2:zmq_ctx_destroy), вызванная в родительском, потоке будет ждать вечно пока не закроются все подключенные потоки.

Это бесчеловечно, заставлять каждого программиста изобретать свой велосипед по завершению программ, но пользуясь языками с автоочисткой, такие танцы с бубном становятся не нужны.

### Зачем вообще нам нужна Зера (Why We Needed ØMQ)

Теперь когда мы видели зеру в действии, давайте разберемся зачем она нужна.

На текущий момент множество приложений завязаны на сетевой взаимодействие, будь то внутренняя сеть или интернет. Множество разработчиков бьются над проблемой обмена сообщениями. Кто-то использует готовые продукты очередей, но чаще всего пишутся свои велосипеды поверх протоколов TCP и UDP. Это довольно простые протоколы, но пересылка нескольких байт из точки А в точку Б может существенно отличаться и теряется надежность и гибкость.

Давайте рассмотрим типичные проблемы с которыми мы сталкиваемся при работе через чистый TCP. Любой модуль, реализующий работу с сообщениями, должен решать  большинство из нижеперечисленных проблем.


1. Как мы будем обрабатывать ввод-вывод? Осуществлять блокировку и обработку в коде своего приложения или делегируем это в отдельный слой? Это архитектурный вопрос. Блокирование ввода/вывода приводит к жесткой, не масштабируемой архитектуре. Однако решение с отдельным слоем обработки очень тяжело корректно реализовать.

2. Сможем ли мы обрабатывать динамические сообщения, то есть то, что выходит за рамки шаблонных. Можем ли мы разделить клиенты и серверы, и ожидать что серверы никогда не исчезнут? А что если нам понадобится соединить сервер с сервером? Можем ли мы переподключаться через каждые несколько секунд?

3. Каким образом нам преобразовывать сообщение для передачи через сеть? Как нам поделить передаваемые данные таким образом, чтобы было легко читать и записывать не опасаясь за переполнение буфера, чтобы это было эффективно для маленьких данных, но адекватным для больших видюшек танцующих котиков в шляпах?

4. Как нам обрабатывать сообщения, которые требуют немедленной отправки? В частности, когда мы ждем, что сдохший компонент снова оживет? Должны ли мы отменить сообщение, положить его в базу данных или же в очередь на оперативной памяти?

5. Где нам хранить очередь сообщений? Что делать если один из компонентов читающих из очереди очень медленный и забивает своим чтением всю нашу очередь? Как мы будем от этого защищаться?

6. Что нам делать с потерянными сообщениями? Будем ли мы ждать обновления данных, запрашивать переотправку данных или же мы реализуем отдельный слой, который будет отвечать за гарантированную доставку сообщения? А что если этот слой и развалится?

7. Что будет если нам понадобится использовать разные транспортные протоколы? Скажем широковещательный, а не одноадресный TCP? Или к примеру IPv6? Нужно ли переписывать приложение или достаточно будет изменить абстрактный слой?

8.  Как нам маршрутизировать сообщения? Можем ли мы отправить одно сообщение множеству подключений? Можем ли мы ответить первоначальному отправителю сообщения?

9. Как нам обмениваться сообщениями между приложениями реализованными на разных языках программирования? Можем ли мы переписать протокол отправки или просто пересобрать библиотеку? Если первое, то как при этом гарантировать стабильность стека сообщений? Если второе, то как гарантировать совместимость?

10. Как представлять сообщение, которое может быть прочитано в разных архитектурах? Можем ли мы использовать строгую типизацию?

11. Как нам обрабатывать сбои в сети? Будем ли мы ждать или повторять действие, тихонечко игнорировать или вообще отменять операцию?

Возьмем типовой опенсорсный проект, такой как [Hadoop Zookeeper](http://hadoop.apache.org/zookeeper/) и почитаем код на Си в файле [src/c/src/zookeeper.c](http://github.com/apache/zookeeper/blob/trunk/src/c/src/zookeeper.c). Когда я читал этот код, в Январе 2013, было примерно 4200 строк загадочного не задокументированного кода, который реализовывал общение клиента с сервером. Я увидел плюс в том что он использует pool вместо select'a. Однако он должен использовать общий слой для работы и строго документированный протокол обмена сообщениями. Совершенно недопустимо каждый раз изобретать собственный велосипед снова и снова.

Но как сделать общий слой обмена сообщениями? Почему, когда разработчикам требуется обмен сообщениями, они реализовывают это поверх чистого TCP и решают все перечисленные проблемы снова и снова?

Оказывается реализация многоразовых систем обмена сообщениями это не так то просто, поэтому многие FOSS(открытое свободное по) проекты пытавшиеся это сделать, проваливались, а коммерческие проекты были дико дорогими,сложными, хрупкими и не гибкими. В 2006 году iMatix разработала [AMQP](http://www.amqp.org/), и раздал его разработчикам FOSS, возможно первый в своем роде рецепт для создания универсального обмена сообщениями. [AMQP](http://www.amqp.org/) работает лучше многих других подобных конструкций, [но остается достаточно сложным, дорогим и хрупким](http://www.imatix.com/articles:whats-wrong-with-amqp/). Требуются недели на то чтобы разобраться и месяцы чтобы построить стабильную архитектуру, которая не падает при увеличении функционала.

###### Рисунок 7 - Как мы представляем обмен в начале (Messaging as it Starts)

![](https://github.com/imatix/zguide/raw/master/images/fig7.png)

Множество проектов по обмену сообщениями, такие как AMQP, пытающихся решить весь список проблем, чтобы пойти по пути пере используемого уровня, вводят новый принцип называемый брокером("broker"), который занимается адресацией, маршрутизацией и очередью. Это позволяет протоколу Клиент/Сервер или набору API над не задокументированным протоколом, общаться через этого брокера. Брокер, отличная штука, снижающая сложность работы с сетью. Но добавление концепции брокера в такие проекты как Zookeeper, сделает его более кривым нежели улучшит. Это означет, что появится еще одна точка отказа. Брокер быстро становится узким горлышком проекта и соответственно добавляет риски. Если приложение позволяет, мы можем предположить что добавив второй, третий, четвертый брокер мы построим таким образом отказоустойчивую схему. Но это не так. На практике это приводит к большому количеству подвижных, жестко связанных частей приложения, которые могут сломаться.

Концепция с брокером в центре системы, требует задействовать всю нашу команду. Мы буквально вынуждены денно и нощно следить за брокерами и бить палками, чтобы они работали. Вам нужны под них контейнеры, резервные копии этих контейнеров, а также специальный человек, который за это все добро отвечает. Так стоит поступать только для действительно больших приложений, со множеством распределенных частей, построенных множеством людей за долгие годы работы.

###### Рисунок 8 - Во что превращается обмен по итогу (Messaging as it Becomes)

![](https://github.com/imatix/zguide/raw/master/images/fig8.png)

Разработчики небольших приложений попадают в ловушку. Если они избегают сетевого обмена и строят монолиты, то приложения оказываются хрупкими, не расширяемыми, а также тяжелыми для сопровождения. Либо же они идут по пути использования обмена сообщениями, делая приложение более масштабируемым и завязываются на дорогостоящую, тяжело поддерживаемую технологию. Ни один из вариантов не решает проблему, возможно по этому технология обмена сообщениями застряла в прошлом веке и вызывает кучу эмоций: негативные у пользователей и позитивные у тех кто продает этим пользователям техническую поддержку.

Что же нам действительно нужно, так это нечто выполняющее работу по обмену сообщениями между разными приложениями, со стоимостью стремящейся к нулю. Это должна быть библиотека, на которую достаточно ссылаться в коде, без каких либо дополнительных зависимостей. Без добавления дополнительных подвижных кусочков кода, создающих дополнительные риски отказа приложения. Она должна быть кроссплатформенной и мультиязычной.

И это ZeroMQ: Эффективная, встраиваемая библиотека, которая решает большинство проблем связанных с обменом по сети, без особых затрат.

А именно:

- Асинхронно обрабатывает потоки ввода/вывода в фоновых потоках. Общение с потоками приложения происходит через не блокируемые структуры, что обеспечивает конкурентные потоки без необходимости блокировок, семафоров и других всевозможных статусов.

- Компоненты могут подключаться и отключаться динамически и Зера автоматически переподключится. Это означает, что вы можете запустить компонент когда вам вздумается. Вы можете построить сервисно-ориентированную архитектуру, в которой компоненты могут присоединяться когда им вздумается

- Сообщения помещаются в очередь когда это необходимо. Зера поступает интеллектуально, отправляя сообщения так быстро, как это возможно, до того как поместить их в очередь.

- Зера имеет механизм который помогает при переполнении очереди, так называемую ватерлинию. Она блокирует отправителей или же выбрасывает сообщения, в зависимости от выбранного паттерна обмена сообщениями.

- Позволяет обмениваться между приложениями через абстракцию, не зависимо от того какой протокол используется: TCP, широковещательный ("multicast"), внутрипроцессный ("in-process" внутри одного процесса), межпроцессный ("inter-process" - между разными процессами). При этом для того чтобы пользоваться разными протоколами не придется вносить изменения в ваш код.

- Безопасно обрабатывает чтение долгих/блокируемых потоков, используя различные стратегии в зависимости от выбранного паттерна обмена

- Позволяет гибко настраивать маршрутизацию ваших сообщений используя разные типы подключений, таких как запрос-ответ или издатель-подписчик. Такие шаблоны отражают топологию вашего сетевого обмена.

- Позволяет создавать прокси серверы для очередей, перенаправления, или упаковать пачку сообщений в одиночный вызов. Прокси могут помочь снизить сложность межсетевых соединений.

- Доставляет сообщения в том виде, в котором вы их отправили, используя простейший принцип передачи пакетов по сети. Если вы отправили сообщение в 10 кб, то по сети будет передано также 10 кб.

- Не накладывает ограничений на формат и размер пересылаемых данных. Можно передать от нуля до гигабайт данных. Нет ограничений на верхнеуровневые структуры, вы можете использовать все что угодно например msgpack, Google's protocol buffers и тд.

- Интеллектуально обрабатывает сетевые ошибки, пытаясь переотправить сообщения если это имеет смысл.

- Меньше загрязняет окружающую среду. Зера меньше нагружает ваши системники, а следовательно потребляет меньше энергии и меньше загрязняет окружающую среду.

На самом деле Зера может куда больше перечисленного. Она оказывает сильное влияние на то, как вы строите свои приложения. Если кратко, это API поверх сокетов, а вам всего лишь нужно оперировать  [zmq_recv()](http://api.zeromq.org/3-2:zmq_recv) и [zmq_send()](http://api.zeromq.org/3-2:zmq_send). Однако рано или поздно, обмен сообщениями становится центральным звеном программы и разбивается на набор подзадач. И это естественный процесс тут нечего бояться. С Зерой это легко масштабируется: каждая из задач сопоставляется узлу, узел общается с другим узлом через произвольный транспорт. При этом нет необходимости задумываться как их делить, зера с этим справится сама. Два узла на процесс (значит узел это поток), если два узла на сервер (значит узел это процесс), или два узла на сеть (значит узел это сервер), при это ничего в коде менять не надо.

## Расширяемость сокетов (Socket Scalability)

Давайте посмотрим на расширяемость Зеры в действии. Ниже приведен shell скрип, параллельно запускающий сервер и пачку клиентов.

```
wuserver &
wuclient 12345 &
wuclient 23456 &
wuclient 34567 &
wuclient 45678 &
wuclient 56789 &
```
Как только мы запустились, можно посмотреть активность процессов командой top. Вополнив команду мы увидим нечто похожее (На четырех ядерной системе)

```
PID  USER  PR  NI  VIRT  RES  SHR S %CPU %MEM   TIME+  COMMAND
7136  ph   20   0 1040m 959m 1156 R  157 12.0 16:25.47 wuserver
7966  ph   20   0 98608 1804 1372 S   33  0.0  0:03.94 wuclient
7963  ph   20   0 33116 1748 1372 S   14  0.0  0:00.76 wuclient
7965  ph   20   0 33116 1784 1372 S    6  0.0  0:00.47 wuclient
7964  ph   20   0 33116 1788 1372 S    5  0.0  0:00.25 wuclient
7967  ph   20   0 33072 1740 1372 S    5  0.0  0:00.35 wuclient
```

Давайте разберемся что же тут произошло. Погодный сервер имеет всего один сокет, и отправляет данные клиентам параллельно. У нас могут быть тысячи параллельно подключенных клиентов. Сервер не видит их и не общается с ними напрямую. По сути сокет зеры это маленький сервер, тихонечко принимающий запросы и отправляющий ответы так быстро, насколько это позволяет сетевое соединение. И этот многопоточный сервер отжирает больше вашего процессора.

## Обновление с ZeroMQ v2.2 до ZeroMQ v3.2 (Upgrading from ZeroMQ v2.2 to ZeroMQ v3.2)

### Совместимые изменения (Compatible Changes)

Эти изменения не влияют на код непосредственно
- Фильтрация издатель/подписчик (pub-sub) перенесена на стророну издателя. Это позволяет существенно повысить производительность в большинстве случаев. Вы можете безопасно использовать версии v3.2 и v2.1/v2.2 одновременно, не беспокоясь о совместимости. ZeroMQ v3.2 получила множество новых API (zmq_disconnect(), zmq_unbind(), zmq_monitor(), zmq_ctx_set(), и тд.).

### Несовместимые изменения (Incompatible Changes)

- Изменены методы отправки/получения(send/recv): zmq_send() и zmq_recv() теперь отличаются, старый интерфейс и поведение теперь реализованы в методах zmq_msg_send() и zmq_msg_recv(). Симптомы: Ошибка компиляции. Решение: исправьте методы в коде.
- Эти две функции возвращали положительное число при успешной обработке и -1 при ошибке. В v2.x они всегда возвращают 0 при успешной обработке. Симптомы: Получение ошибки при успешной работе. Решение: Строго проверяйте на -1, а не на не нулевое значение.
- zmq_poll() сейчас ожидает миллисекунда, а не микросекунды как было раньше. Симптомы: Приложение перестало отвечать (По факту отвечает, но в 1000 раз медленнее.). Решение: Используйте макрос ZMQ_POLL_MSEC до вызова zmq_poll().
- ZMQ_NOBLOCK сейчас называется ZMQ_DONTWAIT. Симптомы: Ошибка помпиляции на строке ZMQ_NOBLOCK.
- Параметр сокета ZMQ_HWM разделен на два ZMQ_SNDHWM и ZMQ_RCVHWM. Симптомы: Ошибка компиляции на строке макроса ZMQ_HWM.
- Большинство, но не все, параметров zmq_getsockopt() сейчас имеют тип integer. Симптомы: Ошибка во время выполнения, при вызове zmq_setsockopt или zmq_getsockopt.
- Параметр ZMQ_SWAP был удален. Симптомы: Ошибка во время компиляции. Решение: Переделайте свой код.

###  Рекоммендации по макросам (Suggested Shim Macros)

Для тех кто хочет работать на двух версиях сразу, мы советует эмулировать третью версию используя макросы, если это конечно позволяет язык. Вот определения макросов C, которые помогают вашему C/C++ коду работать в обеих версиях (взято из [CZMQ](http://czmq.zeromq.org/)):

```
#ifndef ZMQ_DONTWAIT
#   define ZMQ_DONTWAIT     ZMQ_NOBLOCK
#endif
#if ZMQ_VERSION_MAJOR == 2
#   define zmq_msg_send(msg,sock,opt) zmq_send (sock, msg, opt)
#   define zmq_msg_recv(msg,sock,opt) zmq_recv (sock, msg, opt)
#   define zmq_ctx_destroy(context) zmq_term(context)
#   define ZMQ_POLL_MSEC    1000        //  zmq_poll is usec
#   define ZMQ_SNDHWM ZMQ_HWM
#   define ZMQ_RCVHWM ZMQ_HWM
#elif ZMQ_VERSION_MAJOR == 3
#   define ZMQ_POLL_MSEC    1           //  zmq_poll is msec
#endif
```

## Внимание: Разногласие парадигм! (Warning: Unstable Paradigms!)

Традиционная сетевая разработка строится на утверждении, что один сокете это одно соединение с одним клиентом. Существуют широковещательные протоколы, но это скорее экзотика. Когда мы утверждаем "одно соединение = один сокет", мы масштабируем наши приложения только определенным образом. Мы завязываемся на логику где один поток это один сокет с одним плиентом. Мы начинаем мыслить этим соглашением.

Во вселенной ZeroMq сокеты это проход к быстрому, маленькому, фоновому движку, который обеспечивает механизм обмена за вас. Вы не видите как они работают, открывают, закрывают соединение. Независимо от того используете ли вы блокировку при отправке/получении или же пулл(poll), вы делаете это через сокет, а не через соединение. Реализация соединений инкапсулирована от вас и это ключ к масштабированию Зеры.

Поскольку ваш код общается только с сокетом, за ним может скрываться сколько угодно подключений на различных протоколах, что для вас остается прозрачным. Шаблоны предоставляемые ZeroMQ куда легче масштабируются, нежели шаблоны которые вы бы создавали у себя в коде.

Таким образом устоявшееся соглашение что один сокет это одно соединение больше не действует. Когда вы читаете код примеров ваш мозг пытается сопоставить это с тем что вы уже знаете. Вы читаете socket и думаете "а, это означает подключение к другому узлу". Вы ошибаетесь. Вы читаете thread и думаете "а, это означает подключение к другому узлу", и ваш мозг снова вас обманывает.

Если вы только читаете это руководство или может используете зеру первые день-два или может даже три-четыре, вы чувствуете себя не в своей такрелке. Вы пытаетесь построить приложение на тот манер к которому превыкли и у вас ничего не работает. Вас смущает, что зера делает за вас много вещей и все становится слишком просто. Но однажды вы осознаете преимущества и произойдет сдвиг устоявшейся парадигмы в вашем мозгу. И вот тогда то все встанет на своим места.








































