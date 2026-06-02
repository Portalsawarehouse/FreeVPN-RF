# Протоколы и их настройка

## VLESS + Reality (рекомендуется)

Самый устойчивый протокол к блокировкам РКН в 2026 году.
Маскируется под реальный TLS-трафик популярных сайтов (youtube.com, microsoft.com и др.).

**Клиенты:** Hiddify, v2rayNG, Nekoray, Sing-box

Пример конфига:
```json
{
  "type": "vless",
  "tag": "vless-reality",
  "server": "SERVER_IP",
  "server_port": 443,
  "uuid": "UUID",
  "flow": "xtls-rprx-vision",
  "tls": {
    "enabled": true,
    "server_name": "www.microsoft.com",
    "utls": { "enabled": true, "fingerprint": "chrome" },
    "reality": {
      "enabled": true,
      "public_key": "PUBLIC_KEY",
      "short_id": "SHORT_ID"
    }
  }
}
```

---

## Hysteria2

Протокол на базе UDP/QUIC. Очень быстрый, хорошо обходит DPI.
Рекомендуется при медленных соединениях или высоком ping.

**Клиенты:** Hiddify, Nekoray, Sing-box

Пример конфига:
```yaml
server: SERVER_IP:PORT
auth: PASSWORD
tls:
  sni: example.com
  insecure: false
socks5:
  listen: 127.0.0.1:1080
http:
  listen: 127.0.0.1:8080
```

---

## Shadowsocks 2022

Обновлённая версия SS с улучшенной маскировкой.
Простая настройка, работает на большинстве устройств.

**Формат ссылки:**
```
ss://METHOD:PASSWORD@SERVER:PORT#ALIAS
```

---

## WireGuard

Быстрый и простой протокол. Менее устойчив к блокировкам, но обеспечивает максимальную скорость там, где работает.

Конфиг импортируется через QR-код или файл `wg0.conf`.

---

## Выбор протокола по ситуации

| Ситуация | Рекомендация |
|----------|:---:|
| Обычный интернет дома | VLESS+Reality |
| Мобильная сеть (МТС, Билайн, МегаФон) | Hysteria2 |
| Корпоративная / офисная сеть | VMESS+WS+TLS (порт 443) |
| Стриминг / максимальная скорость | WireGuard |
| Всё заблокировано | Hysteria2 + obfs |
