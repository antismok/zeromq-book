# zmq_ctx_set(3)

## Краткое описание
zmq_ctx_set - Устанавливает параметр контекста

## Синопсис
```
int zmq_ctx_set (void *context, int option_name, int option_value);
```

## Описание
Функция zmq_ctx_set() устанавливает параметр, указанный аргументом option_name, в значение аргумента option_value.

Функция zmq_ctx_set() принимает следующие параметры:

- #### ZMQ_BLOCKY: Изменяет поведение блокировки
По умолчанию после вызова *zmq_ctx_term* контекст блокируется навсегда. Это сделано для того, чтобы резкое завершение не привело к потере сообщений. Большинство реальных приложений используют некую форму хендшейка для гарантии, что все клиенты получили сигнал о завершении и только после этого удаляют контекст установив *ZMQ_LINGER* в ноль на всех сокетах. Этот параметр самый простой способ сделать тоже самое. Когда *ZMQ_BLOCKY* установлен в false, все новые сокеты получают задержку(linger) равную нулю. Но вам все равно нужно закрыть все сокеты до удаления контекста.
**Значаение по умолчанию: true (старое поведение).**

- #### ZMQ_IO_THREADS: Устанавливает количество потоков ввода вывода.
Параметр **ZMQ_IO_THREADS** определяет размер пула потоков ØMQ для обработки ввода-вывода. Если ваше приложение использует только *inproc* (межпроцесный) транспорт, то вам стоит установить этот параметр в ноль, иначе он должен быть не меньше единицы. Это параметр необходимо устанавливается до создания сокетов в этом контексте.
**Значаение по умолчанию: 1**

- #### ZMQ_THREAD_SCHED_POLICY: Установить политику планирования для потоков ввода/вывода.
Параметр **ZMQ_THREAD_SCHED_POLICY** устанавливает политику планирования для пула потоков внутренних контекстов. Этот параметр не поддерживается для windows. Поддерживаемые значения можно найти в файле sched.h или на странице http://man7.org/linux/man-pages/man2/sched_setscheduler.2.html. Этот параметр устанавлиется только перед созданием сокета в контексте.
**Значаение по умолчанию: -1**

- #### ZMQ_THREAD_PRIORITY: Устанавлиевает приоритет для потоков ввода/вывода.
Параметр **ZMQ_THREAD_PRIORITY** Аргумент устанавливает приоритет планирования для пула потоков внутренних контекстов. Этот параметр не поддерживается для windows. Поддерживаемые значения можно найти в файле sched.h или на странице http://man7.org/linux/man-pages/man2/sched_setscheduler.2.html. Этот параметр устанавлиется только перед созданием сокета в контексте.
**Значаение по умолчанию: -1**

- #### ZMQ_MAX_MSGSZ: Устанавливает максимальный размер сообщения
Аргумент ZMQ_MAX_MSGSZ устанавливает максимально разрешенный размер пересылаемого сообщения в контексте. Вы можете узнать текущий лимит на сообщения вызвав [zmq_ctx_get(3)](zmq_ctx_get.md) с аргументом ZMQ_MAX_MSGSZ.
**Значаение по умолчанию: INT_MAX**
**Максимально возможное: INT_MAX**

- #### ZMQ_MAX_SOCKETS: Устанавливает ограничение на количество сокетов.
Аргумент ZMQ_MAX_MSGSZ устанавливает лимит на количество сокетов в контексте. Вы можете узнать текущее ограничение вызвав [zmq_ctx_get(3)](zmq_ctx_get.md) с аргументом **ZMQ_SOCKET_LIMIT**.
**Значаение по умолчанию: 1024**

- #### ZMQ_IPV6: Устанавливает параметр IPv6

Параметр ZMQ_IPV6 устанавливает значение ZMQ_IPV6 на все сокеты которые будут созданы после его установки. Значение 1 означает, что IPv6 включен, а 0 означает, что используетсято только IPv4. Когда IPv6 включен, сокет может подключаться или принимать подключения как по IPv4 так и по IPv6.
**Значаение по умолчанию: 0**

## Возвращаемое значение
zmq_ctx_set() - возвращает ноль в случае успеха. В противном случае возвращает -1 и устанавливает errno в одно из значений перечисленных ниже.

## Ошибки
- **EINVAL**
	Запрашиваемый параметр не существует.
    
## Пример
Утсановка ограничения на количество сокетов.
```
void *context = zmq_ctx_new ();
zmq_ctx_set(context, ZMQ_MAX_SOCKETS, 256);
int max_sockets = zmq_ctx_get(context, ZMQ_MAX_SOCKETS);
assert (max_sockets == 256);
```
## Смотрите также
[zmq_ctx_get(3)](zmq_ctx_get.md) [zmq(7)](zmq.md)

## Authors
Страница написана сообществом ØMQ. Для внесения измененй ознакомьтесь с политикой для контрибьюторов ØMQ на страницу [http://www.zeromq.org/docs:contributing.](http://www.zeromq.org/docs:contributing)
Перевел Сарицкий Роман <saritskiy.r@gmail.com>