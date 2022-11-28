
Запускаем OneLiner соединение
------------------------------------

Заходим в root по sudo su в корневой папке

Конфигурация:

открываем файл конфигурации в nano редакторе:

	nano /etc/wireguard/OneLiner.conf

Записываем конфигурацию в файл

	[Interface]
	Address = ...
	DNS = 1.1.1.1
	PrivateKey = ...
	MTU = 1280
	
	[Peer]
	PublicKey = ...
	PresharedKey = ...
	AllowedIPs = 0.0.0.0/0, ::/0
	Endpoint = ...
	PersistentKeepalive = 25

Сохраним конфигурацию и добавим службу в автозагрузку, одновременно запустив ее:

	systemctl enable --now wg-quick@OneLiner




команда запуска службы VPN Wireguard

	wg-quick up OneLiner

команда остановки службы  VPN Wireguard

	wg-quick down OneLiner


При данной конфигурации не работает основной интернет.

Заменяем 

	AllowedIPs = 10.77.77.0/24, 192.168.1.0/24


	[Interface]
	Address = ...
	DNS = 1.1.1.1
	PrivateKey = ...
	MTU = 1280
	
	[Peer]
	PublicKey = ...
	PresharedKey = ...
	AllowedIPs = 10.77.77.0/24, 192.168.1.0/24
	Endpoint = ...
	PersistentKeepalive = 25
