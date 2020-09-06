# SMTP 이메일 보내기

> 사전작업 at gmail

1.IMAP설정
- gmail -> setting -> imap허용

2.보안 수준이 낮은 앱 허용

3.캡챠 잠금해제

## django에서 제공하는 EmailMessage 이용
```python
# settings.py

EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'

EMAIL_USE_TLS =True
EMAIL_HOST = 'smtp.gmail.com'

EMAIL_HOST_USER = '사용하려는 이메일'
EMAIL_HOST_PASSWORD = '패스워드'
EMAIL_PORT = 587


DEFAULT_FROM_EMAIL = EMAIL_HOST_USER
```

```python
# test at shell
from django.core.mail import EmailMessage
email = EmailMessage('제목', '내용', to=['gt0305@likelion.org'])
email.send()
```

_html format으로도 보내보자_
```python
from django.core.mail import EmailMultiAlternatives

subject = 'hello!!!!!!!!!'
from_email = None
to = ['gt0305@likelion.org', 'gt0305@naver.com']
text_content = 'This is an important message.'
html_content = """\
<p>This is an <strong>important</strong> message.</p>
"""
msg = EmailMultiAlternatives(subject, text_content, from_email, to)
msg.attach_alternative(html_content, "text/html")
msg.send()
```