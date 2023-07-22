##  Директория для SSL сертификатов 
- 1 Необходимо установить центр сертификации.

```
./mkcert.exe --install
```
<br>

- 2 Сгенерировать сертификаты, указав домен/поддомен

```
./mkcert.exe *.dom.dev
```
<br>

- 3 Полученные файлы переносим в эту директорию <br>
    _wildcard.yure_domen.pem <br>
    _wildcard.yure_domen-key.pem