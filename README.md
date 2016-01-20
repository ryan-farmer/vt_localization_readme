# localization
Human-readable interface text and translations.

##Overview

The source language file for each project can be located from the root of this repository using the following convention: 
```sh
projects/NAMEOFPROJECT/en_US/intlData.json
```
VoiceThread resource files are simple key-value, UTF-8 encoded [JSON]. The files may or may not contain nested structures. Leaf values are the translatable strings. Translatable strings may contain text, HTML or formatted messages. 

Formatted messages utilize [ICU Message Formatting] for pluralization and value interpolation. Generally, text contained within ```{}``` should be understood to contain a message that will be contain variables or is being formatted for plurals. 
[VoiceThread branded terms] are not subject to translation and should remain in en_US regardless of the target langauge. 

###Examples 

###### Please forgive any language errors in the following examples. Google Translate was used to translate into the various languages. The focus should be on looking for what changes vs. what stays the same in the formatted messages. 

####Key-value pair: 

```"shareWith": "Share a VoiceThread with {name}"```

In this case ```shareWith``` is a key. Keys should never be translated.  ```Share a VoiceThread with {name}``` is the translatable value with a simple variable.

####Simple variable: 

```"shareWith": "Share a VoiceThread with {name}"```

In this key-value case, ```{name} ``` should not be translated. The formatter will eventually replace ```{name} ``` with whatever value has been passed (Homer, Lisa, Bart, etc).

ES: ```"shareWith": "Compartir una VoiceThread con {name}"```

FR: ```"shareWith": "Partager un VoiceThread avec {name}"```

PT: ```"shareWith": "Compartilhar um VoiceThread com {name}"```

In all of the above, ```{name}``` is the only thing that won't get translated. It can be placed wherever necessary to fit the construct of the target language. 

####Plurals: 

Plurals add an additional set of ```{}```. There are some basic rules for handling the plural cases. Most of VoiceThread's plural cases will be ```=1``` and ```other```. Formatting for plurals will usually start with the following ```{count, plural,```. On occasion ```count``` could be something else but ```, plural,``` indicates we are pluralizing. 

#####Simple plural-
```"share": "Share {count, plural, =1 {this VoiceThread}\n other {these VoiceThreads}}"```

The variable ```count``` resolves to a number, ```plural``` indicates we'll be choosing a pluralized form. In this case, ```{this VoiceThread}``` will be selected by the formatter if ```count``` is equal to 1 and ```{these VoiceThreads}```if ```count``` is anything else.  In either case, the only words that need translation in the above are example are *Share*, *this VoiceThread*, and *these VoiceThreads*. 

ES: ```"share": "{count, plural, =1 {Compartir este VoiceThread}\n other {Comparte éstos VoiceThreads}}"```

FR: ```"share": "Partagez {count, plural, =1 {cet VoiceThread}\n other {ces VoiceThreads}}"```

PT: ```"share": "{count, plural, =1 {Partilha isto VoiceThread}\n other {Compartilhe estes VoiceThreads}}"```


#####Plural with interpolated value-

```"success": "{count, plural, =1 {User}\n other {# Users}} successfully copied."```

Similar to the above example, this will show a one form for times when the ```count``` is 1 and another if ```count``` is anything else. The difference is found with the use of the ```#```. Hashtags can be thought of as the ```count``` itself. If count was set to 10 via the associated input, we expect to see ```10 Users successfully copied.``` result when the formatting is finished and the message is displayed to the user. When translating, hashtags should be placed wherever the value of ```count``` makes sense for the target language inside the formatted message. 

ES: ```"success": "{count, plural, =1 {Usuario copiado con éxito}\n other {# Usuarios copian correctamente}}"```

FR: ```"success": "{count, plural, =1 {Utilisateur copié avec succès}\n other {# Utilisateurs copiés avec succès}}"```

PT: ```"success": "{count, plural, =1 {Usuário copiado com êxito}\n other {# Usuários copiado com êxito}}"```


#####NOTE: *It is important that new line, ```\n```, delimiters be kept where they exist in relation to the ```}``` which they follow.* 

#####Plural and variable: 

```"minute": "{count} minute{count, plural, =1 {}\n other {s}}",```

In this case ```count``` is used in two ways: first as a simple varible that will just be shown and second as the determinant for plurals. So if ```count``` was 10, ```10 minutes``` is expected to be the resulting string. In this case, if it made sense for the target language to have the equivalent of ```minutes 10``` be shown to the user then moving ```{count}``` in the target resource value is appropriate.

ES: ```"minute": "{count} minuto{count, plural, =1 {}\n other {s}}",```

FR: ```"minute": "{count} minute{count, plural, =1 {}\n other {s}}",```

PT: ```"minute": "{count} minuto{count, plural, =1 {}\n other {s}}",```

####HTML: 

```"videoNotSupported": "Sorry, your browser doesn't support embedded videos, but don't worry, you can <a href=\"{preview}\">download it</a>."```

In this example, HTML is a part of the value and ```{preview}``` is a value passed in that will result a URL. HTML itself should not be modified. Text that resides in between closing caret brackets, i.e. ```download it``` is translatable. 

ES: ```"videoNotSupported": "Lo sentimos, su navegador no soporta vídeos incrustados, pero no se preocupe, puede <a href=\"{preview}\">descargalo</a>."```

FR: ```"videoNotSupported": "Désolé, votre navigateur ne supporte pas les vidéos intégrées, mais ne vous inquiétez pas, vous pouvez<a href=\"{preview}\">télécharge le</a>."```

PT: ```"videoNotSupported": "Desculpe, seu navegador não suporta vídeos incorporados, mas não se preocupe, você pode <a href=\"{preview}\">baixe</a>."```

[ICU Message Formatting]:<http://userguide.icu-project.org/formatparse/messages>
[JSON]: <http://www.json.org/>
[VoiceThread branded terms]: <https://docs.google.com/spreadsheets/d/1c05Ht5qrq5XO3v_Er88vlfZ4JnfBoxz7IIPQZCZYMtc/edit>
