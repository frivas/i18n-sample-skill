# This is a sample skill that shows how to internationalize it - the easy eay.

### Install python-i18n

`$ pip install python-i18`

Or 

`$ pip install -r requirements.txt -t .`

### Create a folder where all files with the translated strings will be places
`$ mkdir translations`

### Create the correspondent JSON files for each language to be supported. For example:

```
$ touch es-ES.json
$ touch en-US.json
```

### Using as an example the Hello World Skill:

**en-US.json**

```
{
    "WELCOME_MESSAGE": "Welcome, you can say Hello or Help. Which would you like to try?",
    "HELLO_MSG": "Hello Python World from Classes!",
    "HELP_MSG": "You can say hello to me! How can I help?",
    "GOODBYE_MSG": "Goodbye!",
    "REFLECTOR_MSG": "You just triggered %{intent}",
    "ERROR": "Sorry, I had trouble doing what you asked. Please try again."
}
```


**es-ES.json**

```
{
    "WELCOME_MESSAGE": "Te damos la bienvenida, puedes decir Hola o Ayuda, ¿qué deseas hacer?",
    "HELLO_MSG": "Hola!",
    "HELP_MSG": "Puede saludarme, ¿en que te puedo ayudar?",
    "GOODBYE_MSG": "Hasta Luego!",
    "REFLECTOR_MSG": "Acabas de iniciar ${intent}",
    "ERROR": "Perdona, no te he entendido, inténtalo de nuevo por favor."
}
```


### Import the package i18n
`import i18n`

### Add the configuration needed to make i18n work as we need:

```
1. i18n.load_path.append('./translations')
2. i18n.set('skip_locale_root_data', True)
3. i18n.set('file_format', 'json')
4. i18n.set('filename_format', '{locale}.{format}')
```

- Line 1: Tells the package where to look for the translations.
- Line 2: Configures i18n to skip the root of the JSON file.
- Line 3: Configures i18n to use JSON instead of the default YAML.
- Line 4: Tells i18n what is the format of the filename. In this case it can be es.json or es-ES.json.


### Add a request interceptor to get the locale of the request every time. Using the AbstractRequestInterceptor class.

```
1. class LocalizationInterceptor(AbstractRequestInterceptor):
2.     def process(self, handler_input):
3.         locale = handler_input.request_envelope.request.locale
4.        i18n.set('locale', locale)
```

- Line 1: Get the locale from the request everytime.
- Line 2: Configures i18n to use that locale which matches the name of each supported translated language.


### Using the translated strings is as follows:

`speak_output = i18n.t(‘<etiqueta>’)`

`i.e: speak_output = i18n.t('WELCOME_MESSAGE')`

### When using placeholders:

`speak_output = i18n.t(‘<etiqueta>’, <placeholder_name>=‘<value>’)`

```
i.e: intent_name = ask_utils.get_intent_name(handler_input)
      speak_output = i18n.t('REFLECTOR_MSG', intent=intent_name)
```
