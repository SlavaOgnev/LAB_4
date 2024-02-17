# Лабораторная работа №4
Создадим docker image (образ). Для этого понадобится написать Dockerfile. Создаём пустой текстовый документ, где в первую очередь указываем, на основе какого образа будет работать наш. Далее в него установим пакет cowsay и пакет для работы с пингом.
```
touch Dockerfile
gedit Dockerfile

```
![](https://github.com/SlavaOgnev/LAB_4/blob/main/скрины%20для%204/IMAGE%202024-02-17%2014%3A51%3A28.jpg)
#### На этом Dockerfile готов, закрываем и сохраняем его под этим названием. В терминале в папке с этим файлом запускаем команду сборки образа с тегом “cowsay”.
```
docker build -t cowsay .
```
#### Далее запускаем контейнер на основе созданного образа. При создании контейнера передаём ему запуск приложения “cowsay”, которое находится в папке /usr/games и передаём приложению команду "Moo".
```
docker run cowsay /usr/games/cowsay "Moo"
```
![](https://github.com/SlavaOgnev/LAB_4/blob/main/скрины%20для%204/Снимок%20экрана%202024-02-16%20в%2000.56.16.png)
Далее можем подключиться запустить контейнер и  подключиться к нему напрямую командой
```
docker run -it cowsay
```
Запустим два контейнера в рабочем состоянии
![](https://github.com/SlavaOgnev/LAB_4/blob/main/скрины%20для%204/Снимок%20экрана%202024-02-17%20в%2014.56.45.png)

Пропишем `docker ps` и увидем два наших рабочих контейнера:
![](https://github.com/SlavaOgnev/LAB_4/blob/main/скрины%20для%204/Снимок%20экрана%202024-02-17%20в%2014.58.26.png)

#### Следующий шаг это создание сети и добавление наших контейнеров в сеть:
![](https://github.com/SlavaOgnev/LAB_4/blob/main/скрины%20для%204/Снимок%20экрана%202024-02-17%20в%2015.00.37.png)

При помощи команды мы можем увидеть настройки нашей сети:
```
docker network inspect myNetwork
```
![](https://github.com/SlavaOgnev/LAB_4/blob/main/скрины%20для%204/Снимок%20экрана%202024-02-17%20в%2015.02.27.png)
#### В настройках сети мы видим пинг наших подключенных контейнеров. В моем случае 172.22.0.2 и 172.22.0.3

Теперь наша задача проверить с помощью утилиты ping соединение наших контейнеров. Используем команду:
```
docker exec -it cowsay_container ping <IP-адрес_другого_контейнера>
```
Отлично, все работает
![](https://github.com/SlavaOgnev/LAB_4/blob/main/скрины%20для%204/Снимок%20экрана%202024-02-17%20в%2015.07.28.png)


