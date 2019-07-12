# hw30-mail

Запуск **vagrant up**

Лог telnet:
```
MacBook-Pro-Vasilij:Documents vvlasov$ telnet localhost 25
Trying ::1...
Connected to localhost.
Escape character is '^]'.
220 otus.test ESMTP Postfix
HELO otus.test
250 otus.test
MAIL FROM: <info@otus.test>
250 2.1.0 Ok
RCPT TO: <info@otus.test>
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: TestMail
This is a test!!
.
250 2.0.0 Ok: queued as 61BD72063821
quit
221 2.0.0 Bye
Connection closed by foreign host.
```

Само письмо:
```
From info@otus.test  Sat Jul  6 17:58:33 2019
Return-Path: <info@otus.test>
X-Original-To: info@otus.test
Delivered-To: info@otus.test
Received: from otus.test (localhost [IPv6:::1])
        by otus.test (Postfix) with SMTP id 61BD72063821
        for <info@otus.test>; Sat,  6 Jul 2019 17:57:09 +0000 (UTC)
Subject: TestMail
Message-Id: <20190706175722.61BD72063821@otus.test>
Date: Sat,  6 Jul 2019 17:57:09 +0000 (UTC)
From: info@otus.test

This is a test!!
```
