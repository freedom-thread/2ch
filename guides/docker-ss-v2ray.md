## Гайд по быстрой установке shadowsocks+v2ray (Docker)

### Содержание:
1. [Создание виртуальной машины](docker-ss-v2ray.md#создание-виртуальной-машины)
2. [Установка shadowsocks](docker-ss-v2ray.md#установка-shadowsocks)
3. [Запуск shadowsocks](docker-ss-v2ray.md#запуск-shadowsocks)
3. [Подключение клиентов](docker-ss-v2ray.md#подключение-клиентов)


### Создание виртуальной машины
Регистрируемся в любом облаке, после чего cоздаём виртуальную машину из образа Debian 11

После того как создалась виртуальная машина важно не забыть открыть входящий TCP и UDP порт 8388 в админке облака для этой машины

Далее заходим либо через консоль виртуальной машины, либо через SSH

### Установка shadowsocks
После того как зашли в коммандную строку виртуальной машины, выполняем следующие комманды:

`sudo su`

`apt update && apt install -y docker.io`

`docker pull yunielrc/shadowsocks-rust-server`

### Запуск shadowsocks

`docker run --name ss-v2ray -p 8388:8388/tcp -p 8388:8388/udp -e SS_PLUGIN=v2ray-plugin -e SS_PASSWORD=$(openssl rand -base64 12) -e SS_PLUGIN_OPTS=server -d yunielrc/shadowsocks-rust-server`

Показать пароль от shadowsocks:

`docker exec ss-v2ray env | grep SS_PASSWORD | cut -d= -f2`

Порт: `8388`

Метод шифрования: `aes-256-gcm`

Адрес shadowsocks соответствует внешнему адресу виртуальной машины

### Подключение клиентов
Настройка клиентов не входит в этот гайд, однако, я хотел бы порекомендовать несколько хороших клиентов для популярных платформ:

[SagerNet](https://f-droid.org/packages/io.nekohasekai.sagernet/) для Android

[shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows/releases) с плагином [v2ray-plugin](https://github.com/shadowsocks/v2ray-plugin/releases) для Windows

[v2rayA](https://v2raya.org/en/docs/prologue/introduction/) для Linux
