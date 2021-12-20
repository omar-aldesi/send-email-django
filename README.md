# send-email-django
send emails

imoprt:
from django.core.mail import send_mail,send_mass_mail

now in setting.py:

```python
#DataFlair
EMAIL_BACKEND =
‘django.core.mail.backends.smtp.EmailBackend’
EMAIL_HOST = ‘smtp.gmail.com’
EMAIL_USE_TLS = True
EMAIL_PORT = 587
EMAIL_HOST_USER = ‘your_account@gmail.com’
EMAIL_HOST_PASSWORD = ‘your account’s password’
```

now in forms.py

```python
class Subscribe(forms.Form):
    Email = forms.EmailField()
    def __str__(self):
        return self.Email
```

now in views.py:

```python
from django.shortcuts import render
from myproject.settings import EMAIL_HOST_USER
from . import forms
from django.core.mail import send_mail
# Create your views here.
#DataFlair #Send Email
def subscribe(request):
    sub = forms.Subscribe()
    if request.method == 'POST':
        sub = forms.Subscribe(request.POST)
        subject = 'Welcome to DataFlair'
        message = 'Hope you are enjoying your Django Tutorials'
        recepient = str(sub['Email'].value())
        send_mail(subject, 
            message, EMAIL_HOST_USER, [recepient], fail_silently = False)
        return render(request, 'subscribe/success.html', {'recepient': recepient})
    return render(request, 'subscribe/index.html', {'form':sub})
```

to send mass email:

```python
def subscribe(request):
    sub = Subscribe()
    if request.method == 'POST':
        sub = Subscribe(request.POST)
        subject = 'Welcome to DataFlair'
        message = 'Hope you are enjoying your Django Tutorials ()'+str(time.ctime())
        recepient = str(sub['Email'].value())
        datatuple = (subject, message, EMAIL_HOST_USER, ['omar.desi.100@gmail.com','ofadi9383@gmail.com'])
        send_mass_mail((datatuple,), fail_silently=False)
        return render(request, 'success.html', {'recepient': recepient})
    return render(request, 'home.html', {'form':sub})
```

that's it!
