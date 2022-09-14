
# OpenSSL -> Documentation for lammers

## About OpenSSL

OpenSSL — это криптографический инструментарий, реализующий сетевые протоколы Secure Sockets Layer (SSL v2/v3) и Transport Layer Security (TLS v1) и соответствующие им стандарты криптографии.

-> SSL, or Secure Sockets Layer, is an encryption-based Internet security protocol. It was first developed by Netscape in 1995 for the purpose of ensuring privacy, authentication, and data integrity in Internet communications. SSL is the predecessor to the modern TLS encryption used today.

-> SSL is the direct predecessor of another protocol called TLS (Transport Layer Security). In 1999 the Internet Engineering Task Force (IETF) proposed an update to SSL. Since this update was being developed by the IETF and Netscape was no longer involved, the name was changed to TLS.

-> SSL has not been updated since SSL 3.0 in 1996 and is now considered to be deprecated. There are several known vulnerabilities in the SSL protocol, and security experts recommend discontinuing its use. In fact, most modern web browsers no longer support SSL at all.

-> TLS is the up-to-date encryption protocol that is still being implemented online, even though many people still refer to it as "SSL encryption." This can be a source of confusion for someone shopping for security solutions. The truth is that any vendor offering "SSL" these days is almost certainly providing TLS protection, which has been an industry standard for over 20 years. But since many folks are still searching for "SSL protection," the term is still featured prominently on many product pages.

## Practise

Dictionary:
`openssl list -commands`

# Task exec

1. В используемой операционной системе создать каталог (папку) с именем CA (CA - Certification authority).

CMD: `mkdir ca`
CMD: `cd ca`

2. С помощью команды openssl genpkey и соответствующих параметров сгенерировать секретный ключ для алгоритма RSA длиной 2048 бит и сохранить его в каталоге с именем CA.

CMD: `openssl genpkey -algorithm RSA -out <filename>.key`
COMMENT: Опция -out указывает на имя файла для сохранения, без этой опции файл будет выведен в стандартный вывод (на экран). Имя выходного файла не должно совпадать с именем входного файла.
COMMENT: Для безопасности ключа его следует защитить паролем. Генерация приватного ключа RSA используя 128-битное AES шифрование (-aes-128-cbc) и парольную фразу "hello" (-pass pass:hello)
COMMENT CMD: `openssl genpkey -algorithm RSA -out rootCA.key -aes-128-cbc -pass pass:hello`

COMMENT: `Если для генерируемого ключа не указано количество бит, то по умолчанию используется 2048, вы можете указать другое количество бит с помощью команды вида (будет создан 4096-битный ключ)`
COMMENT CMD: `openssl genpkey -algorithm RSA -out rootCA.key -pkeyopt rsa_keygen_bits:4096`

3. С помощью команды openssl rsa и соответствующих параметров вывести информацию о сгенерированном секретном ключе и проанализировать его структуру.

CMD: `openssl rsa -text -in <file>.key`
Output: `
Private-Key: (2048 bit, 2 primes)
modulus:
    00:dc:61:54:91:7e:d8:ea:13:84:aa:8d:18:70:68:
    9f:82:4f:35:c1:d5:90:c4:e9:65:e6:01:58:a6:fe:
    fb:76:b2:9b:3a:52:ba:f2:35:25:28:16:bc:7c:a5:
    dd:2a:8b:e0:de:db:b2:4a:22:1c:5c:4c:06:60:af:
    f0:68:74:d7:0b:db:73:19:e5:92:c5:6e:29:d5:25:
    a0:46:01:f4:d4:ec:f3:c9:07:ee:b0:98:ef:6e:01:
    12:31:61:91:0b:2e:a5:a1:8e:e8:f3:0a:19:4b:53:
    da:05:fb:20:c1:4b:27:bd:a3:80:02:58:fc:dd:f4:
    75:22:61:75:2c:1c:e0:2f:48:c4:e4:ca:69:d9:a5:
    f4:91:3f:e2:ef:bc:33:26:d8:de:39:7c:32:2b:60:
    ad:a5:76:62:12:8d:c0:7c:70:4f:99:ad:34:09:40:
    ed:41:c9:df:34:00:f2:9f:15:94:10:4c:65:ae:9b:
    43:59:00:09:4a:dc:bb:e0:f5:3d:13:72:76:3e:4e:
    b4:c4:8b:f5:3d:00:05:bc:37:56:61:1f:ad:a9:3a:
    7e:bd:18:c7:94:05:ea:33:c6:62:e4:65:f0:aa:67:
    db:09:d5:f6:40:81:0b:9e:56:53:67:35:63:0b:21:
    9c:56:25:a8:e2:07:b4:28:4a:27:02:a4:9e:6a:6f:
    25:bf
publicExponent: 65537 (0x10001)
privateExponent:
    07:6a:f7:8d:f7:06:23:64:96:ef:cc:1d:94:b0:2d:
    69:27:86:64:0d:81:01:e3:30:ff:12:94:ab:d4:08:
    54:a9:f9:f1:2d:d6:6a:0f:61:75:4b:57:31:8c:50:
    8b:18:dc:5d:78:8e:0f:d2:4f:1b:a4:7e:07:52:1d:
    df:87:5c:69:f5:8b:60:0e:b4:15:5e:27:d4:2b:56:
    d6:38:fb:eb:c7:b2:4d:43:bf:df:a9:6b:e1:b8:f1:
    5d:2e:4a:9c:e4:d0:8f:20:a5:19:a8:93:b8:18:71:
    60:07:bb:d8:4c:9a:f3:0d:38:99:52:7c:c3:4d:3b:
    18:63:f2:1b:a5:5d:75:8e:7e:66:c7:d8:df:cb:ad:
    cc:22:3a:9d:5a:df:59:9f:25:71:20:57:4a:ff:6c:
    4a:46:93:d4:b6:ef:c5:93:14:4d:37:ae:c5:bc:61:
    30:ed:76:d8:6a:4d:26:34:15:30:08:ed:2b:41:00:
    01:ee:fa:4f:8b:da:aa:a6:83:55:07:e3:83:96:d0:
    90:32:5c:d7:7d:a5:f9:f1:c2:c6:a9:b4:c2:af:24:
    10:44:7e:69:91:bc:6f:72:3c:de:bc:fb:39:c6:40:
    23:59:a7:88:fe:43:43:d7:c4:ea:45:69:62:71:95:
    97:1b:00:18:7d:39:0b:b1:f5:a2:a3:ba:f2:18:fb:
    55
prime1:
    00:fb:44:9a:00:d4:c5:28:33:ee:47:c6:0c:38:9d:
    15:ba:d2:d4:ae:79:bd:3b:71:fc:2a:ae:3e:d1:4a:
    42:0d:0e:9a:e4:34:fe:9b:6f:95:3f:56:29:e0:f1:
    99:bf:5d:13:41:8b:61:fa:57:02:c2:1f:d7:6f:c0:
    57:7a:d3:cf:3f:4b:72:4d:23:59:6c:00:04:f8:b9:
    7a:15:e4:06:51:7a:e5:97:a6:af:8f:4a:a5:00:62:
    3a:59:6e:98:c7:f4:d4:9d:58:d0:a3:2a:93:2f:ae:
    ac:49:52:d3:59:39:23:6b:13:34:c6:7f:ac:75:7d:
    63:f9:48:eb:7a:1c:22:d7:25
prime2:
    00:e0:87:d0:7e:26:0b:c2:6e:46:95:ea:0b:14:66:
    ce:76:63:1f:98:54:06:d1:8e:27:44:e0:bb:cc:cb:
    3e:87:9b:db:f9:ef:a1:22:25:85:37:0b:8e:30:9c:
    eb:66:cd:85:36:b7:cc:8e:7d:10:24:1e:2d:8c:f5:
    37:9c:73:cd:3a:68:6c:7f:5a:3b:8a:c9:ea:d7:35:
    d9:47:09:ae:23:4f:ec:5a:80:a4:03:0d:ab:73:5e:
    10:87:c6:ac:47:84:17:2a:f8:81:e2:a5:fa:e4:a7:
    12:06:32:0d:d7:89:8c:31:7f:16:14:84:f8:0c:e6:
    48:8f:49:b5:4f:7f:2c:16:13
exponent1:
    7c:2a:e0:77:bc:ad:59:3a:a0:6b:b3:80:e2:91:2d:
    e5:ce:bd:ef:22:95:d2:c4:77:3a:98:34:ce:b4:05:
    83:f2:4d:b4:ac:43:8d:88:4c:96:a9:fb:b3:ff:70:
    5c:d2:9f:eb:69:f7:97:00:5c:8a:95:b5:9e:b1:cc:
    09:14:96:7b:ce:ca:c3:37:ce:be:c2:1b:b2:d5:e5:
    70:df:e8:07:67:d6:01:65:0b:a8:a1:d8:7c:22:0e:
    77:97:61:c4:9e:46:5b:23:42:a6:ff:29:11:0d:1e:
    72:75:8d:9f:af:ce:c2:e1:10:d9:6e:ca:48:9d:18:
    44:5e:36:8f:77:4b:f8:49
exponent2:
    00:bf:e3:32:4a:ed:26:f5:a6:9b:0a:79:f7:b8:1a:
    d8:6e:12:ee:a8:97:7f:30:4e:65:bf:16:b5:49:23:
    95:af:fd:82:b5:0a:97:52:00:70:e6:07:29:20:e0:
    aa:c9:b3:f1:1a:3f:60:41:92:1e:5e:4f:b0:2c:1c:
    51:c7:92:ac:1d:33:ab:2d:f7:a6:95:49:55:3b:51:
    98:fc:7e:08:65:c3:63:42:41:58:6a:07:9f:b4:3b:
    fa:b2:9f:17:13:13:8f:5d:38:fe:7f:fd:cb:fa:e7:
    d1:9e:9b:de:7a:8a:e1:d6:57:3f:3e:90:19:11:a5:
    28:f3:d4:51:70:bc:45:a8:23
coefficient:
    7f:50:dd:73:d7:16:a4:94:61:22:f5:eb:78:43:e4:
    3a:4a:2b:b9:bf:38:81:98:ea:88:39:32:07:e7:47:
    5f:6b:d6:e7:bb:ce:fe:b8:b5:92:91:53:12:cc:34:
    c3:b7:ba:33:14:2f:01:1b:5a:c7:8a:87:c5:20:c1:
    71:c8:c5:ad:f1:44:61:23:ac:61:c6:c2:20:aa:89:
    d5:3e:eb:4a:02:b3:db:d5:bc:e3:3d:44:3a:47:b9:
    ff:04:e6:eb:4e:f3:49:23:48:e4:ab:7d:da:6a:c5:
    65:18:8c:96:31:70:67:cd:c2:7e:d4:db:55:c8:d0:
    95:4b:22:4f:b5:da:7a:e6
writing RSA key
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQDcYVSRftjqE4Sq
jRhwaJ+CTzXB1ZDE6WXmAVim/vt2sps6UrryNSUoFrx8pd0qi+De27JKIhxcTAZg
r/BodNcL23MZ5ZLFbinVJaBGAfTU7PPJB+6wmO9uARIxYZELLqWhjujzChlLU9oF
+yDBSye9o4ACWPzd9HUiYXUsHOAvSMTkymnZpfSRP+LvvDMm2N45fDIrYK2ldmIS
jcB8cE+ZrTQJQO1Byd80APKfFZQQTGWum0NZAAlK3Lvg9T0TcnY+TrTEi/U9AAW8
N1ZhH62pOn69GMeUBeozxmLkZfCqZ9sJ1fZAgQueVlNnNWMLIZxWJajiB7QoSicC
pJ5qbyW/AgMBAAECggEAB2r3jfcGI2SW78wdlLAtaSeGZA2BAeMw/xKUq9QIVKn5
8S3Wag9hdUtXMYxQixjcXXiOD9JPG6R+B1Id34dcafWLYA60FV4n1CtW1jj768ey
TUO/36lr4bjxXS5KnOTQjyClGaiTuBhxYAe72Eya8w04mVJ8w007GGPyG6VddY5+
ZsfY38utzCI6nVrfWZ8lcSBXSv9sSkaT1LbvxZMUTTeuxbxhMO122GpNJjQVMAjt
K0EAAe76T4vaqqaDVQfjg5bQkDJc132l+fHCxqm0wq8kEER+aZG8b3I83rz7OcZA
I1mniP5DQ9fE6kVpYnGVlxsAGH05C7H1oqO68hj7VQKBgQD7RJoA1MUoM+5Hxgw4
nRW60tSueb07cfwqrj7RSkINDprkNP6bb5U/Ving8Zm/XRNBi2H6VwLCH9dvwFd6
088/S3JNI1lsAAT4uXoV5AZReuWXpq+PSqUAYjpZbpjH9NSdWNCjKpMvrqxJUtNZ
OSNrEzTGf6x1fWP5SOt6HCLXJQKBgQDgh9B+JgvCbkaV6gsUZs52Yx+YVAbRjidE
4LvMyz6Hm9v576EiJYU3C44wnOtmzYU2t8yOfRAkHi2M9Tecc806aGx/WjuKyerX
NdlHCa4jT+xagKQDDatzXhCHxqxHhBcq+IHipfrkpxIGMg3XiYwxfxYUhPgM5kiP
SbVPfywWEwKBgHwq4He8rVk6oGuzgOKRLeXOve8ildLEdzqYNM60BYPyTbSsQ42I
TJap+7P/cFzSn+tp95cAXIqVtZ6xzAkUlnvOysM3zr7CG7LV5XDf6Adn1gFlC6ih
2HwiDneXYcSeRlsjQqb/KRENHnJ1jZ+vzsLhENluykidGEReNo93S/hJAoGBAL/j
MkrtJvWmmwp597ga2G4S7qiXfzBOZb8WtUkjla/9grUKl1IAcOYHKSDgqsmz8Ro/
YEGSHl5PsCwcUceSrB0zqy33ppVJVTtRmPx+CGXDY0JBWGoHn7Q7+rKfFxMTj104
/n/9y/rn0Z6b3nqK4dZXPz6QGRGlKPPUUXC8RagjAoGAf1Ddc9cWpJRhIvXreEPk
Okorub84gZjqiDkyB+dHX2vW57vO/ri1kpFTEsw0w7e6MxQvARtax4qHxSDBccjF
rfFEYSOsYcbCIKqJ1T7rSgKz29W84z1EOke5/wTm607zSSNI5Kt92mrFZRiMljFw
Z83CftTbVcjQlUsiT7XaeuY=
-----END PRIVATE KEY-----
`

4. С помощью команды openssl rsa и соответствующих параметров извлечь открытый ключ и сохранить его в каталоге с именем CA

CMD: `openssl rsa -in <private_file>.key -pubout -out <public_file>.key`

5. С помощью команды openssl rsa и соответствующих параметров вывести информацию об извлеченном открытом ключе и проанализировать его структуру.

CMD: `openssl rsa -text -in <file_public>.key -pubin`

COMMENT: -pubin делает так, что вместо приватного ключа читается открытый ключ

OUTPUT: `
Public-Key: (2048 bit)
Modulus:
    00:dc:61:54:91:7e:d8:ea:13:84:aa:8d:18:70:68:
    9f:82:4f:35:c1:d5:90:c4:e9:65:e6:01:58:a6:fe:
    fb:76:b2:9b:3a:52:ba:f2:35:25:28:16:bc:7c:a5:
    dd:2a:8b:e0:de:db:b2:4a:22:1c:5c:4c:06:60:af:
    f0:68:74:d7:0b:db:73:19:e5:92:c5:6e:29:d5:25:
    a0:46:01:f4:d4:ec:f3:c9:07:ee:b0:98:ef:6e:01:
    12:31:61:91:0b:2e:a5:a1:8e:e8:f3:0a:19:4b:53:
    da:05:fb:20:c1:4b:27:bd:a3:80:02:58:fc:dd:f4:
    75:22:61:75:2c:1c:e0:2f:48:c4:e4:ca:69:d9:a5:
    f4:91:3f:e2:ef:bc:33:26:d8:de:39:7c:32:2b:60:
    ad:a5:76:62:12:8d:c0:7c:70:4f:99:ad:34:09:40:
    ed:41:c9:df:34:00:f2:9f:15:94:10:4c:65:ae:9b:
    43:59:00:09:4a:dc:bb:e0:f5:3d:13:72:76:3e:4e:
    b4:c4:8b:f5:3d:00:05:bc:37:56:61:1f:ad:a9:3a:
    7e:bd:18:c7:94:05:ea:33:c6:62:e4:65:f0:aa:67:
    db:09:d5:f6:40:81:0b:9e:56:53:67:35:63:0b:21:
    9c:56:25:a8:e2:07:b4:28:4a:27:02:a4:9e:6a:6f:
    25:bf
Exponent: 65537 (0x10001)
writing RSA key
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA3GFUkX7Y6hOEqo0YcGif
gk81wdWQxOll5gFYpv77drKbOlK68jUlKBa8fKXdKovg3tuySiIcXEwGYK/waHTX
C9tzGeWSxW4p1SWgRgH01OzzyQfusJjvbgESMWGRCy6loY7o8woZS1PaBfsgwUsn
vaOAAlj83fR1ImF1LBzgL0jE5Mpp2aX0kT/i77wzJtjeOXwyK2CtpXZiEo3AfHBP
ma00CUDtQcnfNADynxWUEExlrptDWQAJSty74PU9E3J2Pk60xIv1PQAFvDdWYR+t
qTp+vRjHlAXqM8Zi5GXwqmfbCdX2QIELnlZTZzVjCyGcViWo4ge0KEonAqSeam8l
vwIDAQAB
-----END PUBLIC KEY-----
`

6. С помощью команды openssl rsa и соответствующих параметров зашифровать секретный ключ с помощью алгоритма 3DES.

NOT WORKING :()
CMD: `openssl rsa -des3 -in <private_file>.key -out <des3_private>.key`
ALT CMD: `openssl rsa -in key.pem -des3 -out keyout.pem`

SUCSESS CMD's: `openssl des3 -in private.key -out private_des3.key`
SUCSESS CMS's2: `openssl des3 -d -in private_des3.key -out private_des3_dec.key`
