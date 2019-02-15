# Proyecto DocenciaMD

mdx-edx es una plantilla HTML5 desarrollada en el formato de Mako Templates para 
DocenciaMD. La estructura de archivos es la misma que la plantilla original open-edx.

Para instalar la plantilla, clonar el repositorio en la ruta donde estará instalado: 
/ruta/de/instalacion/mdx-edx con esta estructura:

```
-/ruta/de/instalacion
  |-mdx-edx/
    |-cms/
      |-static/
      |-templates/
    |-lms/
      |-static/
      |-templates/
```

Verificar en los archivos lms.env.json y cms.env.json que la variable de temas 
personalizados este activada:

```
"COMPREHENSIVE_THEME_DIRS": [
    "/edx/app/edxapp/edx-platform/themes",
],
"ENABLE_COMPREHENSIVE_THEMING": true,
"DEFAULT_SITE_THEME": "mdx-edx",
```

Aplicar la plantilla desde el panel de control de Django a través de un túnel SSH y 
compilar la plantilla del LMS y CMS en caso de haber realizado cambios. El proceso tarda 5-10 minutos en completarse mientras se generan los static assets:

```
$ sudo -H -u edxapp bash 
$ source /edx/app/edxapp/edxapp_env
$ cd /edx/app/edxapp/edx-platform
$ paver update_assets lms settings=aws
$ paver update_assets cms settings=aws
$ exit
```

Durante la compilación el sitio estará inaccesible. Una vez termine reiniciar los 
servicios

```
$ sudo /edx/bin/supervisorctl restart lms
$ sudo /edx/bin/supervisorctl restart cms
$ sudo /edx/bin/supervisorctl restart edxapp_worker:
```
