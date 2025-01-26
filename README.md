# Proyecto Django con Bootstrap 5

Este proyecto proporciona una guía paso a paso para crear una aplicación Django utilizando **Bootstrap 5** para el diseño de interfaces.

---

## Tabla de Contenidos
- [Requisitos](#requisitos)
- [Configuración del Entorno](#configuración-del-entorno)
- [Instalar Django y Guardar dependencias](#instalar-Django-y-Guardar-dependencias)
- [Pasos del Proyecto](#pasos-del-proyecto)
  - [Configuración Inicial](#configuración-inicial)
  - [Configuración del Proyecto](#configuración-del-proyecto)
  - [Creación de Vistas y Modelos](#creación-de-vistas-y-modelos)
  - [Integración de Bootstrap 5](#integración-de-bootstrap-5)


---

## Requisitos

- Python 3.9 o superior
- Django 4.0 o superior
- Bootstrap 5

---

## Configuración del Entorno

1. Crear el entorno virtual:
   ```bash
   python -m venv venv


## Activación del Entorno

2. Activar el entorno virtual:
    ### Windows
    ```bash
    venv\Scripts\activate

## Configuración Inicial
## Instalar Django y Guardar dependencias

3. Intalación Django
    ```bash
    pip install django

## Guardar las dependencias
4. Instalación dependencias
    ```bash
    pip freeze > requirements.txt

## Pasos del Proyecto
5. Crear el Proyecto
    ```bash
    django-admin startproject my_project

6. Ingresar al directorio del Proyecto
    ```bash
    cd my_proyect

7. Creamos la Aplicación
    ```bash
    python manage.py startapp core

8. Generar las migraciones iniciales
     ```bash
    python manage.py migrate

## Configuración del Proyecto

9. Conectar el proyecto con la aplicación: Agregar 'dia2' en la lista INSTALLED_APPS dentro del archivo leccion2/settings.py:
    ```bash
    INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'core',
    ]

10. Ejecutar el servidor:
    ```bash
    python manage.py runserver

## Creación de Vistas y Modelos
11. Creación de Modelos core/models.py
    ```bash
    class Producto(models.Model):
        nombre = models.CharField(max_length=100)
        precio = models.DecimalField(max_digits=10,decimal_places=2)
        descripcion = models.TextField()
        
        def __str__(self):
            return self.nombre

12. Genero el Archivo Base en la carpeta principal templates/base.html
    ```bash
    <!DOCTYPE html>
    <html>

    <head>
        <title>{% block title %}Tienda Online{% endblock %}</title>
    </head>

    <body>
        {% block content %}{% endblock %}
    </body>

    </html>

13. Configurar templates/index.html
    ```bash
    {% extends 'base.html' %}

    {% block title %}Inicio{% endblock %}

    {% block content %}
    <h1>Bienvenido a la Tienda Online</h1>
    <a href="/producto/">Ver Productos</a>
    {% endblock %}

14. En el templates/productos.html
    ```bash
     {% block title %}Productos{% endblock %}

    {% block content %}
    <h1>Listado de Productos</h1>
    <ul>
        {% for producto in productos %}
        <li>{{ producto.nombre }} - ${{ producto.precio }}</li>
        {% endfor %}
    </ul>
    {% endblock %}

15. Configurar my_proyect/urls.py 
    ```bash
    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('core.urls')),
    ]

16. core/urls.py
    ```bash	
    from django.urls import path
    from .import views

    urlpatterns = [
        path('', views.index, name='index'),
        path('producto/', views.productos, name='productos'),
    ]

15. Crear migraciones
    ```bash
    python manage.py makemigrations
   
16. Aplicar migraciones
    ```bash
    python manage.py migrate

17. Crear un superusuario
    ```bash
    python manage.py createsuperuser

18. Verificamos usuario y contraseña del superuser por motivos de aprendizaje le vamos a dar estos parametros pero que no son seguros
    ```bash
    admin
    admin@gmail.com
    admin1234
    y

19. Registrar el modelo en core/admin.py
    ```bash
    from django.contrib import admin
    from .models import Producto

    admin.site.register(Producto)

21. Active el servidor 
    python manage.py runserver

20. Verifique la vista administrador y sus user y contraseña  http://127.0.0.1:8000/admin

22. Verificamos los productos http://127.0.0.1:8000/producto

