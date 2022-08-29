# Password protect the Jupyter service

This is useful where you want to have a password on a local network install of Jupyter lab.  

I followed these directions, with a couple of tweaks:

[Jupyter and SystemD](https://janakiev.com/blog/jupyter-systemd/)

The exec start has no hyphen in Jupyter Lab: 

`ExecStart=/home/nick/anaconda3/bin/python -m jupyterlab`

## Generating the password 

Nightmarishly difficult but solved [here](https://stackoverflow.com/questions/64299457/jupyter-password-not-hashed) in Stackoverflow:

```python
>>> from notebook.auth import passwd
>>> from notebook.auth.security import passwd_check
>>>
>>> password = 'myPass123'
>>>
>>> hashed_argon2 = passwd(password)
>>> hashed_sha1 = passwd(password, 'sha1')
>>> 
>>> print(hashed_argon2)
argon2:$argon2id$v=19$m=10240,t=10,p=8$JRz5GPqjOYJu/cnfXc5MZw$LZ5u6kPKytIv/8B/PLyV/w
>>>
>>> print(hashed_sha1)
sha1:c29c6aeeecef:0b9517160ce938888eb4a6ec9ca44e3a31da9519
```