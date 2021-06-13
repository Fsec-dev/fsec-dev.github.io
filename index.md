## Hola amigos

Que tal a tod@s, les presento mi sitio Web el cual esta hecho para todas la personas amante de la tecnologia
y el Hacking, este sitio esta en funcionamiento gracias a Github, estare posteando algunos Topics ligado al Hacking
y la programacion, espero que disfruten y aprendan con cada Post. :)

## Topics
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

##Tag

{% for tag in site.tags %}
  <h3>{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}

## Whoami

Soy Andrew Hacker entusiasta, con ligeras tendencias como programador Web (Backend y Frontend), Pitonista de corazon
amante de la musica derivados del genero del Rock. En mi dia a dia uso Debian como sistema base.

**Puedes contactarme usando estas direcciones:** 
- **Email:** ```anonuser_2.0@protonmail.com```
- **Jabber:** ```digitalhardcore@jabber.cz```
- **Telegram:** ```https://t.me/APTDarkLord```
