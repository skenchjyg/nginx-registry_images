# nginx-registry_images
При помощи этого docker-compose.yaml поднимаем nginx и персональный registry для образов docker.
Ниже описана инструкция по запуску, прочитать внимательно, все действия являются обязательными для выполнения.

В папке auth мы храним логин и пароль для того, чтобы можно было залогинится в наш registry, для наполнения файла своими данными необходимо воспользоваться\ http://htpasswd.org  ввести свой логин и пароль и заполнить файл registry.password своими значениями из поля Apache MD5 (ну или воспользоваться другими похожими порталами)\ или можно на своей машине выполнить команду htpasswd -Bc registry.password adminuser, но для запуска потребуется локально установить утилиту apache2-utils,\ мы создаем новый файл с именем registry.password и задаем что пароль делаем для пользователя adminuser, пароль будет запрошен в интерактивном режиме. 

Команды для генерации сертификатов.
Файл nginx-selfsigned.crt необходим для генерации 2х файлов nginx-selfsigned.pem  и  nginx-selfsigned.key которые мы через volumes прокидываем внуттрь контейнера

openssl req -x509 -nodes -sha256 -days 1024 -newkey rsa:2048 -config ./nginx-selfsigned.conf -out /usr/local/share/ca-certificates/nginx-selfsigned.crt
update-ca-certificates
openssl verify /usr/local/share/ca-certificates/nginx-selfsigned.crt
openssl x509 -in /usr/local/share/ca-certificates/nginx-selfsigned.crt -text -noout
cp /etc/ssl/certs/nginx-selfsigned.pem ./
cp /etc/ssl/private/nginx-selfsigned.key ./




Для информации.
В папке Наработки пока наброски, для автоматического создания файла в папке auth который бы создавался в контейнере и просто прокидывался бы в папку через volume.
Как автоматически генерировать сертификаты пока не придумал, собирать свой образ тут нет пока желания.
