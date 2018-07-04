Pipenv: Python Development Workflow for Humans
==============================================

.. image:: https://img.shields.io/pypi/v/pipenv.svg
    :target: https://pypi.python.org/pypi/pipenv

.. image:: https://img.shields.io/pypi/l/pipenv.svg
    :target: https://pypi.python.org/pypi/pipenv

.. image:: https://badge.buildkite.com/79c7eccf056b17c3151f3c4d0e4c4b8b724539d84f1e037b9b.svg?branch=master
    :target: https://code.kennethreitz.org/source/pipenv/

.. image:: https://img.shields.io/pypi/pyversions/pipenv.svg
    :target: https://pypi.python.org/pypi/pipenv

.. image:: https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg
    :target: https://saythanks.io/to/kennethreitz

---------------

**Pipenv** es una herramienta que apunta a traer todo lo mejor del mundo de empaquetado (bundler, composer, npm, cargo, yarn, etc.) al mundo de Python. *Windows es un ciudadano primera-clase en nuestro mundo*

Automáticamente crea y maneja un entorno virtual para tus proyectos, también como agregar/remover paquetes desde tu ``Pipfile`` como instalar/desisntalar paquetes. También genera el más importante ``Pipfile.lock``, que es usado para producir determinado build

.. image:: http://media.kennethreitz.com.s3.amazonaws.com/pipenv.gif

Los problemas que Pipenv busca resolver son multifacéticos

- No necesitas usar más ``pip`` y ``virtualenv`` separados. Trabajan juntos.
- Manejar un archivo ``requirements.txt`` `puede ser problemático <https://www.kennethreitz.org/essays/a-better-pip-workflow>`_, por eso Pipenv usa en su lugar ``Pipfile`` y ``Pipfile.lock``, que son superiores para usos básicos
- Los Hashes se usan en todas partes, siempre. Seguridad. Automáticamente expone vulnerabilidades de seguridad.
- Te da una vista de tu árbol de dependecias (e.g. ``$ pipenv graph``).
- Coordina el  flujo de desarrollo cargando archivos ``.env``.
.. - Streamline development workflow by loading ``.env`` files.

Instalación
------------

Si estas en MacOS, puedes instalar Pipenv fácilmente con Homebrew::

    $ brew install pipenv

O, si estás usando Ubuntu 17.10::

    $ sudo apt install software-properties-common python-software-properties
    $ sudo add-apt-repository ppa:pypa/ppa
    $ sudo apt update
    $ sudo apt install pipenv

De lo contrario, solo usa pip::

    $ pip install pipenv

✨🍰✨


☤ Testimonios de Usuarios
-------------------

**Jannis Leidel**, former pip maintainer—
    *Pipenv is the porcelain I always wanted to build for pip. It fits my brain and mostly replaces virtualenvwrapper and manual pip calls for me. Use it.*

**David Gang**—
    *This package manager is really awesome. For the first time I know exactly what my dependencies are which I installed and what the transitive dependencies are. Combined with the fact that installs are deterministic, makes this package manager first class, like cargo*.

**Justin Myles Holmes**—
    *Pipenv is finally an abstraction meant to engage the mind instead of merely the filesystem.*


☤ Características
----------

- Habilita verdaderos *builds deterministas*, mientras fácilmente especificas *solo lo que quieres*.
- Genera y verifica hashes en los archivos para bloquear dependencias.
- Automáticamente instala la versión de Python, si ``pyenv`` esta disponible
- Automáticamente busca tu proyecto home, recursivamente, buscando por un ``Pipfile``
- Automáticamente genera un ``Pipfile``, si no existe
- Automáticamente crea un entorno virtual en una locación estándar
- Automáticamente agrega/remueve paquetes a un ``Pipfile`` cuando se instala/desinstala
- Automáticamente carga archivos ``.env``, si estos existen.

Los comandos principales son ``install``, ``uninstall`` and ``lock``, el cual genera un ``Pipfile.lock``. Estos tienen la intención de reemplazar el uso de ``$ pip install``, así como manejar manualmente un entorno virtual (para activar uno, corre ``$ pipenv shell``).

Conceptos Básicos
//////////////

- Un entorno virtual se creará automáticamente, cuando no exista.
- Cuando no se pasen parámetros a ``install``, todos los paquetes ``[packages]`` especificados se instalarán.
- Para iniciar un entorno virtual con Python 3, corre ``$ pipenv --three``. 
- Para iniciar un entorno virtual con Python 2, corre ``$ pipenv --two``. 
- De lo contrario, cualquier entorno virtual será por defecto.

Otros Comandos
//////////////

- ``shell`` generará un shell con el entorno virtual activado.
- ``run`` va a correr el comando dado desde el entorno virtual, con algún argumento adelante (e.g. ``$ pipenv run python``)
- ``check`` asegura que los requerimientos en PEP 508 se están cumpliendo en el entorno actual.
- ``graph`` va a imprimir un bonito árbol de todas tus dependencias instaladas.

Completado en Shell
////////////////

Por ejemplo, con fish, coloca esto en tu ``~/.config/fish/completions/pipenv.fish``::

    eval (pipenv --completion)

Alternativamente, con bash, coloca esto en tu ``.bashrc`` o ``.bash_profile``::

    eval "$(pipenv --completion)"


¡Completado en Magic shell ahora estan habilitadas! También hay un `plugin en fish <https://github.com/fisherman/pipenv>`_, el cual automáticamente activa tus subshells por ti!

Fish es la mejor shell. Deberias usarla.

☤ Uso
-------

::

    $ pipenv
    Uso: pipenv [OPCIONES] COMANDO [ARGS]...

    Opciones:
      --where          Muestra la ruta del proyecto.
      --venv           Muestra la ruta donde esta el entorno virtual.
      --py             Muestra la ruta donde esta el interprete de Python.
      --envs           Muestra opciones para variables de entorno.
      --rm             Elimina el entorno virtual.
      --bare           Minimal output.
      --completion     Output completion (to be eval'd).
      --man            Muestra el archivo manual.
      --three / --two  Usa Python 3/2 cuando crea un entorno virtual.
      --python TEXT    Especifica cual versión de Python debería usar el entorno virtual.
      --site-packages  Activa los paquetes de sitio para el entorno virtual.
      --version        Muestra la versión y sale.
      -h, --help       Muestra esta mensaje y sale.


    Ejemplos de Uso:
       Crea un nuevo proyecto usando Python 3.6, especificamente:
       $ pipenv --python 3.6

       Instala todas las dependencias para un proyecto(incluyendo desarrollo):

       $ pipenv install --dev

       Crea un lockfile que contiene prelanzamientos:
       $ pipenv lock --pre

       Muestra un árbol de todas tus dependencias instaladas:
       $ pipenv graph

       Verifica tus dependencias por vulnerabilidades de seguridad:
       $ pipenv check

       Instala un setup.py loca en tu entorno virutal/Pipfle:
       $ pipenv install -e .

       Usa el comando pip de nivel inferior:
       $ pipenv run pip freeze

    Comandos:
      check      Verifica por vulnerabilidades de seguridad y por marcadores en PEP 508 proporcionados en Pipfile.
      clean      Desinstala todos los paquetes especificados en Pipfile.lock.
      graph      Muestra un árbol de dependencias actualmente instaladas.
      install    Instala los paquetes proporcionados y los agrega al Pipfile, o (si no se le da ninguno), 
                 instala todos los paquetes
      lock       Genera un Pipfile.lock.
      open       Muestra un módulo dado en tu editor.
      run        Genera un comando instalado en tu entorno virtual.
      shell      Genera un shell dentro de tu entorno virutal.
      sync       Instala todos los paquetes especificados en Pipfile.lock.
      uninstall  Desinstala un paquete proporcionado y lo elimina del Pipfile.


Localiza tu proyecto::

    $ pipenv --where
    /Users/kennethreitz/Library/Mobile Documents/com~apple~CloudDocs/repos/kr/pipenv/test

Localiza tu entorno virtual::

   $ pipenv --venv
   /Users/kennethreitz/.local/share/virtualenvs/test-Skyy4vre

Localiza tu interprete de Python::

    $ pipenv --py
    /Users/kennethreitz/.local/share/virtualenvs/test-Skyy4vre/bin/python

Instala paquetes::

    $ pipenv install
    Creating a virtualenv for this project...
    ...
    No package provided, installing all dependencies.
    Virtualenv location: /Users/kennethreitz/.local/share/virtualenvs/test-EJkjoYts
    Installing dependencies from Pipfile.lock...
    ...

    To activate this project's virtualenv, run the following:
    $ pipenv shell

Instala un paquete de desarrollo::

    $ pipenv install pytest --dev
    Installing pytest...
    ...
    Adding pytest to Pipfile's [dev-packages]...

Muestra el árbol de dependencias::

    $ pipenv graph
    requests==2.18.4
      - certifi [required: >=2017.4.17, installed: 2017.7.27.1]
      - chardet [required: >=3.0.2,<3.1.0, installed: 3.0.4]
      - idna [required: >=2.5,<2.7, installed: 2.6]
      - urllib3 [required: <1.23,>=1.21.1, installed: 1.22]

Genera un lockfile::

    $ pipenv lock
    Assuring all dependencies from Pipfile are installed...
    Locking [dev-packages] dependencies...
    Locking [packages] dependencies...
    Note: your project now has only default [packages] installed.
    To install [dev-packages], run: $ pipenv install --dev

Instala todas las dependencias de desarrollo::

    $ pipenv install --dev
    Pipfile found at /Users/kennethreitz/repos/kr/pip2/test/Pipfile. Considering this to be the project home.
    Pipfile.lock out of date, updating...
    Assuring all dependencies from Pipfile are installed...
    Locking [dev-packages] dependencies...
    Locking [packages] dependencies...

Desinstala todo::

    $ pipenv uninstall --all
    No package provided, un-installing all dependencies.
    Found 25 installed package(s), purging...
    ...
    Environment now purged and fresh!

Usa el shell::

    $ pipenv shell
    Loading .env environment variables…
    Launching subshell in virtual environment. Type 'exit' or 'Ctrl+D' to return.
    $ ▯

☤ Documentación
---------------

Documentación esta alojada en `pipenv.org <http://pipenv.org/>`_.
