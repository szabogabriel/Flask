# Bootstrap es templatek letrehozasa

A pip-en keresztul feltelepitjuk a flask bootstrap konyvtarat.
`pip install flask-bootstrap`. Ehhez lehet, hogy a rendszergazda
jogosultsagaira lesz szukseg.

Az alap applikacio mappajaba egy uj mappat kell letrehozni `templates`
nev alatt. Ebbe a mappaba pakolhatjuk a sajat templatejeinket. A flask
program automatikusan ezt a mappat keresi a template-ek hasznalatakor.
Pl.

```
C:\Dev\Workspace\Applikacio\app.py
C:\Dev\Workspace\Applikacio\templates\hello.html
```

Az `app.py` peldaul a kovetkezo keppen nezhet ki:

```
from flask import render_template, Flask, escape, request   # a flask reszek importalasa
from flask_bootstrap import Bootstrap                       # a bootstrap importja

app = Flask(__name__)   # applikacio letrehozasa
Bootstrap(app)          # bootstrap inicializacioja

@app.route('/hello/')           # a cimben a http://127.0.0.1:5000/hello cim deklaralasa
@app.route('/hello/<name>')     # a cimben a http://127.0.0.1:5000/hello/<felhasznalo> valtozoval ellatott utvonal deklaracioja
def hello(name=None):           # fuggveny definicioja a 'name' valtozoval mint parameterrel. alapesetben nincs beallitva (None-erteku)
    return render_template('hello.html', name=name)   # a hello.html template-et a name valtozoval rendereljuk
```

A `hello.html` a kovetkezo keppen nezhet ki:

```
{% extends "bootstrap/base.html" %}
{% block title %}This is an example page{% endblock %}

{% block navbar %}
<div class="navbar navbar-fixed-top">
  <!-- ... -->
</div>
{% endblock %}

{% block content %}
  <h1>Hello, from Flask Bootstrap</h1>
  
{% if name %}
  <h1>Greetings, {{ name }}!</h1>
{% else %}
  <h1>Greetings, Anonymous!</h1>
{% endif %}
{% endblock %}
```

Az elso sorban deklaraljuk, hogy a bootstrap template-jet hasznaljuk. Ezt kovetik a blokkok: navigacios es tartalmi.

A `{% if name %}` blokk lekerdezi, hogy letezik-e `name` nevu valtozo.

Az egesz applikaciot klasszikus modon, mint egy flask-appot inditjuk el. Pl.

```
set FLASK_APP=app.py
flask run
```
