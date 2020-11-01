# Самодельные Виртуальные машины для лабораторных работ курсов SUSE

## Описание

Тестовая среда состоит из 2 виртуальных машин с openSuse.

Пользователь    | Пароль
----------------|--------
vagrant         | vagrant
student         | student
root            | redhat

### server1.172.16.1.21.xip.io

* ip: 172.16.1.21
* DNS: dnsmasq 
* vsftpd сервер для репозитория пакетов с dvd диска дистрибутива


### server2.172.16.1.22.xip.io

* ip: 172.16.1.22
* minimal server

## Требования

* Vagrant
* Oracle VirtualBox
* ~ 16 GiB памяти
* ~ 30 GiB на жестком диске

## Установка и настройка

1. [Hashicorp Vagrant](https://www.vagrantup.com/downloads.html)
2. [Cmder](http://cmder.net/), или [Windows Terminal](https://github.com/microsoft/terminal)
3. [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
5. [Этот репозиторий](https://github.com/dmi3mis/SHL)

### Запуск 

```bash
git clone https://github.com/dmi3mis/SHL
cd SHL
vagrant up <имя компьютера>

```

### Снимки состояния

Сразу после успешной установки рекомендуется сохранить состояние виртуальных машин с помощью снимков состояния.
Для этого дайте команду

```bash
vagrant snapshot save [vm-name] snapshot-name
```
Чтобы потом вернуться к ранее сохранённому состоянию машин и не повторять долгую процедуру установки дайте команду.
Не забудьте указать параметр `--no-provision`, чтобы машины только восстановились из ранее сохранённого состояния, запустились и не запускали заново скрипты развертывания.

> ВНИМАНИЕ!
> При возврате к ранее сохранённому снимку все изменения, проделанные с машиной удалятся.
> Чтобы вернуться и не потерять изменения, перед возвратом создайте ещё один снимок под другим именем.

```bash
 vagrant snapshot restore --no-provision [vm-name] snapshot-name
```
