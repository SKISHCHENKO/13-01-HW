# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - Кищенко Сергей FOPS-41


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

# Домашнее задание к занятию «Уязвимости и атаки на информационные системы»

## Задание 1. 

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.  

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.  
Просканируйте эту виртуальную машину, используя nmap.  
Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.  

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.  
Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.  

Ответьте на следующие вопросы:  

Какие сетевые службы в ней разрешены?  
Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)  
Приведите ответ в свободной форме.   
 
## Решение 1

Вывод:  
![Задание 1](https://github.com/SKISHCHENKO/13-01-HW/blob/main/img/task1_1.png)

![Задание 1](https://github.com/SKISHCHENKO/13-01-HW/blob/main/img/task1_2.png)

![Задание 1](https://github.com/SKISHCHENKO/13-01-HW/blob/main/img/task1_3.png)

![Задание 1](https://github.com/SKISHCHENKO/13-01-HW/blob/main/img/task1_4.png)


Проверка произведена с помощью nmap на виртуальной машине Metasploitable2-Linux  
Nmap проверил стандартный диапазон TCP-портов (1–65535).  
1692 порта закрыты (на них нет сервиса или ОС отвечает RST).  
В списке ниже показаны только открытые.  

PORT — порт/протокол (например 21/tcp).  
STATE — состояние (open).  
SERVICE — что это за служба (по сигнатурам).  
VERSION — версия (для поиска уязвимостей).  

1) Какие сетевые службы разрешены   

21/tcp — ftp — vsftpd 2.3.4  
22/tcp — ssh — OpenSSH 4.7p1 Debian 8ubuntu1  
23/tcp — telnet — Linux telnetd  
25/tcp — smtp — Postfix smtpd  
53/tcp — domain (DNS)  
80/tcp — http — Apache httpd 2.2.8 (Ubuntu) DAV/2  
111/tcp — rpcbind — v2 (rpc #100000)  
139/tcp — netbios-ssn — Samba smbd 3.X  
445/tcp — netbios-ssn — Samba smbd 3.X  
512/tcp — exec (rsh/rexec-службы семейства r-сервисов)  
513/tcp — rlogin  
514/tcp — tcpwrapped   
1524/tcp — ingreslock? (bind shell)  
2049/tcp — nfs — 2–4 (rpc #100003)  
2121/tcp — ftp — ProFTPD 1.3.1  
3306/tcp — mysql — MySQL 5.0.51a-3ubuntu5  
3632/tcp — distccd — distccd v1 (GNU) 4.2.4  
5432/tcp — postgresql — PostgreSQL DB  
5900/tcp — vnc — VNC (protocol 3.3)   
6000/tcp — X11 — X (access denied)  
6667/tcp — irc — UnrealIRCd  
8009/tcp — ajp13 (AJP-коннектор)  
  
1) Какие уязвимости были обнаружены  

Уязвимость №1 — vsftpd 2.3.4 (Backdoor Command Execution)  

21/tcp ftp vsftpd 2.3.4  
в определённой сборке vsftpd 2.3.4 был внедрён бэкдор, позволяющий удалённо выполнить команды.  
Ссылка Exploit-DB: https://www.exploit-db.com/exploits/17491  

Уязвимость №2 — ProFTPD 1.3.1 (mod_sql SQL Injection)  

2121/tcp ftp ProFTPD 1.3.1  
SQL-инъекция в модуле mod_sql при обработке имени пользователя (в зависимости от конфигурации).  
Ссылка Exploit-DB: https://www.exploit-db.com/exploits/32798  

Уязвимость №3 — DistCC / distccd (удалённое выполнение команд)  

3632/tcp distccd distccd v1 (GNU) 4.2.4  
демон распределённой компиляции distccd при небезопасной настройке позволяет выполнять команды удалённо.  
Ссылка Exploit-DB: https://www.exploit-db.com/exploits/9915  

## Задание 2. 

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.  

Запишите сеансы сканирования в Wireshark.  

Ответьте на следующие вопросы:  

Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?  
Как отвечает сервер?    
Приведите ответ в свободной форме.   

## Решение 2  
 
атакующая ВМ Linix kali 192.168.56.101  
уязвимая  ВМ Linux Metasploitable2 192.168.56.106  

### 1️⃣ SYN-сканирование  
nmap -sS 192.168.56.106  

┌──(kali㉿kali)-[~]  
└─$ nmap -sS 192.168.56.106  
Starting Nmap 7.95 ( https://nmap.org ) at 2026-01-15 05:10 EST  
Nmap scan report for 192.168.56.106  
Host is up (0.00012s latency).  
Not shown: 977 closed tcp ports (reset)  
PORT     STATE SERVICE  
21/tcp   open  ftp  
22/tcp   open  ssh  
23/tcp   open  telnet  
25/tcp   open  smtp  
53/tcp   open  domain  
80/tcp   open  http  
111/tcp  open  rpcbind  
139/tcp  open  netbios-ssn  
445/tcp  open  microsoft-ds  
512/tcp  open  exec  
513/tcp  open  login  
514/tcp  open  shell  
1099/tcp open  rmiregistry  
1524/tcp open  ingreslock  
2049/tcp open  nfs  
2121/tcp open  ccproxy-ftp  
3306/tcp open  mysql  
5432/tcp open  postgresql  
5900/tcp open  vnc  
6000/tcp open  X11  
6667/tcp open  irc  
8009/tcp open  ajp13  
8180/tcp open  unknown  
MAC Address: 08:00:27:04:E7:92 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)  

Nmap done: 1 IP address (1 host up) scanned in 0.33 seconds  

### 2️⃣ FIN-сканирование  
nmap -sF 192.168.56.106  
 
──(kali㉿kali)-[~]  
└─$ nmap -sF 192.168.56.106  
Starting Nmap 7.95 ( https://nmap.org ) at 2026-01-15 05:10 EST  
Nmap scan report for 192.168.56.106  
Host is up (0.00018s latency).  
Not shown: 977 closed tcp ports (reset)  
PORT     STATE         SERVICE  
21/tcp   open|filtered ftp  
22/tcp   open|filtered ssh  
23/tcp   open|filtered telnet  
25/tcp   open|filtered smtp  
53/tcp   open|filtered domain  
80/tcp   open|filtered http  
111/tcp  open|filtered rpcbind  
139/tcp  open|filtered netbios-ssn  
445/tcp  open|filtered microsoft-ds  
512/tcp  open|filtered exec  
513/tcp  open|filtered login  
514/tcp  open|filtered shell  
1099/tcp open|filtered rmiregistry  
1524/tcp open|filtered ingreslock  
2049/tcp open|filtered nfs  
2121/tcp open|filtered ccproxy-ftp  
3306/tcp open|filtered mysql  
5432/tcp open|filtered postgresql  
5900/tcp open|filtered vnc  
6000/tcp open|filtered X11  
6667/tcp open|filtered irc  
8009/tcp open|filtered ajp13  
8180/tcp open|filtered unknown  
MAC Address: 08:00:27:04:E7:92 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)  

Nmap done: 1 IP address (1 host up) scanned in 1.43 seconds  

### 3️⃣ Xmas-сканирование  
nmap -sX 192.168.56.106  

──(kali㉿kali)-[~]  
└─$ nmap -sX 192.168.56.106  
Starting Nmap 7.95 ( https://nmap.org ) at 2026-01-15 05:10 EST  
Nmap scan report for 192.168.56.106  
Host is up (0.00018s latency).  
Not shown: 977 closed tcp ports (reset)  
PORT     STATE         SERVICE  
21/tcp   open|filtered ftp  
22/tcp   open|filtered ssh  
23/tcp   open|filtered telnet  
25/tcp   open|filtered smtp  
53/tcp   open|filtered domain  
80/tcp   open|filtered http  
111/tcp  open|filtered rpcbind  
139/tcp  open|filtered netbios-ssn  
445/tcp  open|filtered microsoft-ds  
512/tcp  open|filtered exec  
513/tcp  open|filtered login  
514/tcp  open|filtered shell  
1099/tcp open|filtered rmiregistry  
1524/tcp open|filtered ingreslock  
2049/tcp open|filtered nfs  
2121/tcp open|filtered ccproxy-ftp  
3306/tcp open|filtered mysql  
5432/tcp open|filtered postgresql  
5900/tcp open|filtered vnc  
6000/tcp open|filtered X11  
6667/tcp open|filtered irc  
8009/tcp open|filtered ajp13  
8180/tcp open|filtered unknown  
MAC Address: 08:00:27:04:E7:92 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)  

Nmap done: 1 IP address (1 host up) scanned in 1.50 seconds  

### 4️⃣ UDP-сканирование  

──(kali㉿kali)-[~]  
└─$ nmap -sU 192.168.56.106  
Starting Nmap 7.95 ( https://nmap.org ) at 2026-01-15 05:10 EST  
Nmap scan report for 192.168.56.106  
Host is up (0.00038s latency).                                                                 
Not shown: 945 closed udp ports (port-unreach), 51 open|filtered udp ports (no-response)       
PORT     STATE SERVICE                                                                       
53/udp   open  domain                                                                        
111/udp  open  rpcbind                                                                       
137/udp  open  netbios-ns                                                                    
2049/udp open  nfs                                                                           
MAC Address: 08:00:27:04:E7:92 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)             
                                                                                             
Nmap done: 1 IP address (1 host up) scanned in 1018.50 seconds                                
                                                                                    
Файл wireshark со сканирования:  

[Задание 2 — дамп Wireshark](https://raw.githubusercontent.com/SKISHCHENKO/13-01-HW/main/files/wireshark.pcapng)

SYN scan: TCP-пакеты с флагом SYN (0x02) — 1000 запросов  
FIN scan: TCP-пакеты с флагом FIN (0x01) — 1023 запроса  
Xmas scan: TCP-пакеты с флагами FIN+PSH+URG (0x29) — 1023 запроса  
UDP scan: UDP-датаграммы — 1750 запросов  

 Чем отличаются режимы сканирования с точки зрения сетевого трафика  
### 1.SYN scan (nmap -sS)  

Что отправляет Kali: TCP SYN (флаг 0x02) на разные порты цели.  
Kali → Metasploitable: SYN  
Metasploitable → Kali:  

если порт открыт: SYN,ACK (флаги 0x12)  
если порт закрыт: RST,ACK (флаги 0x14)  

23 ответа SYN,ACK (0x12) → 23 открытых TCP-порта  
977 ответов RST,ACK (0x14) → закрытые порты  


### 2.FIN scan (nmap -sF)  

Что отправляет Kali: TCP пакет с FIN (0x01) без установленного соединения.  

закрытый порт должен ответить RST  
открытый порт молчит   

Kali → Metasploitable: много FIN (0x01)  
Metasploitable → Kali: 977 раз RST,ACK (0x14)  


### 3.Xmas scan (nmap -sX)  

Что отправляет Kali: TCP пакет с “ёлочными” флагами FIN+PSH+URG (0x29).  

закрытые → RST  
открытые → нет ответа  

Kali → Metasploitable: флаги 0x29  
Metasploitable → Kali: 977 ответов RST,ACK (0x14)  

### 4.UDP scan (nmap -sU)  

Что отправляет Kali: UDP датаграммы на разные порты.  
UDP не имеет “рукопожатия” и подтверждений как TCP.  

закрытый UDP-порт → сервер отвечает ICMP Destination Unreachable / Port Unreachable  
(ICMP type 3, code 3)  

открытый UDP-порт → молчит (если сервис не отвечает на “пустой” запрос)  

Kali → Metasploitable: 1750 UDP пакетов  
Metasploitable → Kali: 1026 ICMP type=3 code=3 (“port unreachable”)  

  Как отвечает сервер (по фактическим пакетам)  

На SYN scan:  
открытые порты: SYN,ACK (0x12) — 23 раза  
закрытые порты: RST,ACK (0x14) — 977 раз  

На FIN scan:  
закрытые порты: RST,ACK (0x14) — 977 раз  
открытые порты: тишина (ответов нет) → отсюда open|filtered  

На Xmas scan:  
закрытые порты: RST,ACK (0x14) — 977 раз  
открытые порты: тишина → open|filtered  

На UDP scan:  
закрытые UDP-порты: ICMP type 3 code 3 — 1026 раз  
остальное: тишина → open|filtered  

SYN-скан занял примерно 0.04 сек  
FIN-скан ~ 1.10 сек  
Xmas-скан ~ 1.22 сек  
UDP-скан ~ 1018 сек (≈ 17 минут)  





