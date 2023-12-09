## 1. Использование команды cat в Linux

230 mkdir control_work

231 cd control_work/

232 cat > "Домашние животные"
Собаки
Кошки
Хомяки

233 cat > "Вьючные животные"
Лошади
Верблюды
Ослы

234 cat "Домашние животные" "Вьючные животные" > Animals

235 cat Animals
Собаки
Кошки
Хомяки
Лошади
Верблюды
Ослы

236 mv "Animals" "Друзья человека"

237 clear

## 2. Работа с директориями в Linux

238 mkdir folder_for_control_work

239 mv 'Друзья человека' control_work/folder_for_control_work/

240 mv 'Друзья человека' folder_for_control_work/

241 ls

242 cd folder_for_control_work/

243 ls
'Друзья человека'

## 3. Работа с MySQL в Linux. “Установить MySQL на вашу вычислительную машину ”

244 sudo apt-get update

245 sudo apt update

246 sudo apt install mysql

247 sudo apt install mysql-server

248 sudo service mysql status

249 clear

## 4. Управление deb-пакетами

250 wget http://ftp.us.debian.org/debian/pool/main/s/sl/sl_5.02-1_amd64.deb

251 sudo dpkg -i sl_5.02-1_amd64.deb

252 sudo dpkg -r sl

253 clear

## 5. История команд в терминале Ubuntu

254 history
