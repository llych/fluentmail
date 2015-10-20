fluentmail [![Build Status](https://travis-ci.org/alexandrevicenzi/fluentmail.svg?branch=master)](https://travis-ci.org/alexandrevicenzi/fluentmail) [![Version](https://pypip.in/version/fluentmail/badge.png)](https://pypi.python.org/pypi/fluentmail)
==========

Tiny library to send email fluently

## Install

`pip install fluentmail`

or

`python setup.py install`

## Compatibility

Works with Python 2.6+ and PyPy, tested by Travis-CI.

## Usage

### Basic

```python
from fluentmail import *

mail = FluentMail('smtp.gmail.com', 587, TLS)

mail.credentials('you@gmail.com', 'pwd')\
    .from_address('you@gmail.com')\
    .to('other@gmail.com')\
    .subject('FluentMail')\
    .body(u'Hi, I\'m FluentMail.')\
    .send()
```

### To many receptors

```python
from fluentmail import *

mail = FluentMail('smtp.gmail.com', 587, TLS)

mail.credentials('you@gmail.com', 'pwd')\
    .from_address('you@gmail.com')\
    .to('other@gmail.com')\
    .to('another@gmail.com')\
    .subject('FluentMail')\
    .body(u'Hi, I\'m FluentMail.')\
    .send()
```

or

```python
from fluentmail import *

mail = FluentMail('smtp.gmail.com', 587, TLS)

mail.credentials('you@gmail.com', 'pwd')\
    .from_address('you@gmail.com')\
    .to(['other@gmail.com', 'another@gmail.com'])\
    .subject('FluentMail')\
    .body(u'Hi, I\'m FluentMail.')\
    .send()
```

### To, Cc, Bcc and Reply-To

```python
from fluentmail import *

mail = FluentMail('smtp.gmail.com', 587, TLS)

mail.credentials('you@gmail.com', 'pwd')\
    .from_address('you@gmail.com')\
    .to('other@gmail.com')\
    .cc('another@gmail.com')\
    .bcc('moreone@gmail.com')\
    .reply_to('me@gmail.com')\
    .subject('FluentMail')\
    .body(u'Hi, I\'m FluentMail.')\
    .send()
```

### HTML Body

```python
from fluentmail import *

mail = FluentMail('smtp.gmail.com', 587, TLS)

mail.credentials('you@gmail.com', 'pwd')\
    .from_address('you@gmail.com')\
    .to('other@gmail.com')\
    .subject('FluentMail')\
    .body(u'<h2>Hi, I\'m FluentMail.<h2>')\
    .as_html()\
    .send()
```

### With Attachment

```python
from fluentmail import *

mail = FluentMail('smtp.gmail.com', 587, TLS)

mail.credentials('you@gmail.com', 'pwd')\
    .from_address('you@gmail.com')\
    .to('other@gmail.com')\
    .subject('FluentMail')\
    .body(u'<h2>Hi, I\'m FluentMail.<h2>', 'utf-8')\ # Body charset is optional.
    .as_html()\
    .attach('photo.png')\
    .attach('description.txt', 'utf-8')\ # Charset is optional, and only for Text files.
    .send()
```
```python
2015-10-20 修改发送图片显示

from fluentmail import *

mail = FluentMail('smtp.gmail.com', 587, TLS)

mail.credentials('you@gmail.com', 'pwd')\
    .from_address('you@gmail.com')\
    .to('other@gmail.com')\
    .subject('FluentMail')\
    .body(u'<h2>Hi, I\'m FluentMail.<h2> <br><img src="cid:photo.png" border="1"><br>', 'utf-8')\ # Body charset is optional.
    .as_html()\
    .attach('photo.png')\
    .send()

```
### Being more Pythonic

```python
from fluentmail import *

mail = FluentMail('smtp.gmail.com', security=SSL, credentials=('user', 'pwd'))
mail.body(u'<h2>Hi, I\'m FluentMail.<h2>', 'utf-8', True)
mail.send(from_address='you@bar.com',
          to=['other@bar.com', 'me@bar.com'],
          cc=[],
          bcc=[],
          reply_to=[],
          subject='FluentMail')
```

### Authentication type

#### NON_ENCRYPTED

```
mail = FluentMail('smtp.yoursite.com', 25, NON_ENCRYPTED)
```

#### SSL

```
mail = FluentMail('smtp.yoursite.com', 465, SSL)
```

#### TLS

```
mail = FluentMail('smtp.yoursite.com', 587, TLS)
```

By default SSL uses port 465, TLS uses 587 and AUTH 25.

For GMail you may want to read [this](https://www.google.com/settings/security/lesssecureapps) security info.

## Common smtp servers

| Name  | Server | Authentication | Port |
|:----|:--------:|:--------------:|:----:|
|Gmail|smtp.gmail.com|SSL|465|
|Gmail|smtp.gmail.com|StartTLS|587|
|Hotmail|smtp.live.com|SSL|465|
|Mail.com|smtp.mail.com|SSL|465|
|Outlook.com|smtp.live.com|StartTLS|587|
|Office365.com|smtp.office365.com|StartTLS|587|
|Yahoo Mail|smtp.mail.yahoo.com|SSL|465|

## TODO

- Docs
- Unit tests
- Test with others SMTP providers
