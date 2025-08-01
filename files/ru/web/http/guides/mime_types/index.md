---
title: MIME types
slug: Web/HTTP/Guides/MIME_types
---

**Медиа тип** (так же известный как **Multipurpose Internet Mail Extensions** или **MIME тип)** является стандартом, который описывает природу и формат документа, файла или набора байтов. Он определён и стандартизирован в спецификации {{RFC(6838)}} .

Организация [Internet Assigned Numbers Authority (IANA)](https://www.iana.org/) является ответственной за все официально признанные MIME типы, и вы можете найти самый последний и полный лист MIME типов на их странице [Медиа Типов](https://www.iana.org/assignments/media-types/media-types.xhtml).

> **Предупреждение:** **Важно:** Для принятия решения о том, как обрабатывать URL, браузеры используют MIME типы, _а не расширения файлов_, так что серверам необходимо отправлять правильные MIME типы в {{HTTPHeader("Content-Type")}} заголовке ответа. При неточном задавании этого заголовка, браузеры с большой вероятностью будут неправильно интерпретировать и обрабатывать содержание файлов, из-за чего сайт будет работать неверно.

## Структура MIME типа

Простейший MIME тип состоит из _типа_ и _подтипа_ — двух строк разделённых наклонной чертой (`/`), без использования пробелов.

```
тип/подтип
```

**Тип** представляет общую категорию, в которой находится тип данных, например `video` или `text`. **Подтип** же строго отождествляется с отдельным типом данных, представляемых данным MIME типом. Например, для MIME типа `text`, подтипы могут быть `plain` (простой текст), `html` ({{Glossary("HTML")}} source code) или `calendar` (для iCalendar `.ics`).

Необязательный **параметр** может быть добавлен для указания дополнительных деталей

```
тип/подтип;параметр=значение
```

Например, для MIME типов категории `text`, необязательный параметр `charset` может быть задан для уточнения кодировки, используемой в документе. Для объявления, что пересылаемый файл имеет кодировку UTF-8, необходимо использовать MIME тип `text/plain;charset=UTF-8`. При не указании параметра `charset`, его значение автоматически будет задано, как {{Glossary("ASCII")}} (`US-ASCII`), если в настройках браузера не будет определено иначе.

MIME типы являются нечувствительными к регистру, но традиционно их пишут строчными буквами, за исключением значений параметров.

### Типы

Все типы можно разделить на два класса: **дискретные** и **многокомпонентные.** Дискретные типы представляют одиночные файлы, например, одиночный текстовый, музыкальный или видео файл. Многокомпонентные типы представляют документы, составленные из нескольких частей, каждая из которых может иметь свой отдельный MIME тип, или они могут заключать в себе несколько отдельных файлов, передаваемых в одном сообщении. Например, многокомпонентные MIME типы используются для передачи нескольких изображений в одном email.

#### Дискретные типы

В настоящее время на IANA зарегистрированы следующие дискретные типы:

- `application` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#application)
  - : Любой вид бинарных данных, явно не попадающих ни в одну другую группу типов. Данные, которые будут выполняться или как-либо интерпретироваться, или данные для выполнения, которых необходимо отдельное приложение. Для указания базового типа бинарных данных (данных без определённого типа) используют тип `application/octet-stream`. Другие распространённые примеры включают `application/pdf`, `application/pkcs8` и `application/zip`.
- `audio` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#audio)
  - : Аудио или музыкальные данные. Примеры: `audio/mpeg`, `audio/vorbis`.
- `example`
  - : Тип, зарезервированный для написания примеров, отображающих использование MIME типов. Этот тип никогда не должен использоваться вне примеров кода или документации. `example` может так же использоваться, как подтип.
- `font` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#font)
  - : Данные шрифтов. Распространённые примеры включают `font/woff`, `font/ttf` и `font/otf`.
- `image` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#image)
  - : Изображения или графические данные, включая векторную и растровую графику, а так же анимированные версии форматов неподвижных изображений, таких как [GIF](/ru/docs/Glossary/GIF) или APNG. Распространённые примеры включают `image/jpeg`, `image/png`, и `image/svg+xml`.
- `model` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#model)
  - : Данные моделей для 3D объектов или сцен. Примеры: `model/3mf` и `model/vml`.
- `text` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#text)
  - : Любые текстовые данные, так или иначе доступные для чтения человеку, а так же исходный код или текстовые данные для программ. Примеры: `text/plain`, `text/csv` и `text/html`.
- `video` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#video)
  - : Видео данные или файлы. Например, MP4 фильмы (`video/mp4`).

Любые текстовые документы без определённого подтипа стоит отправлять, как `text/plain` тип. Аналогичным образом, `application/octet-stream` тип подойдёт бинарным документам при неопределённом или неизвестном подтипе.

#### Многокомпонентные типы

_Многокомпонентные_ типы описывают категории разграниченных на части документов, где каждая из частей может иметь свой отдельный MIME тип. При работе с электронными письмами, они могут использоваться для описания нескольких отдельных файлов, передаваемых в одном сообщении. Они представляют **составные документы**.

За исключением `multipart/form-data` типа, используемого в {{HTTPMethod("POST")}} методе [HTML форм](/ru/docs/Learn_web_development/Extensions/Forms), и `multipart/byteranges` типа, используемом в ответе {{HTTPStatus("206")}} `Partial Content` для отправки части документа, HTTP никаким особым образом не обрабатывает многокомпонентные типы, и просто отправляет данные в браузер (который, с большой вероятностью, предложит сохранить переданный файл, тоже не зная как его обработать).

Существуют два многокомпонентных типа:

- `message` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#message)
  - : Сообщение, включающее в себя другие сообщения. Этот тип может использоваться, например, для представления сообщения, которое включают в себя другое переадресованное сообщение, как часть данных, или для отправки больших сообщений по частям, как если бы каждое сообщение отправлялось отдельно. Примеры включают `message/rfc822` (для переадресованных или цитируемых сообщений) и `message/partial` для автоматического разделения одного большого сообщения на несколько небольших и их последующей сборки на стороне получателя.
- `multipart` [Список IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#multipart)
  - : Данные составленные из нескольких компонентов, каждый из которых может иметь отдельный MIME тип. Примеры включают `multipart/form-data` (для данных созданных с помощью {{domxref("FormData")}} API) и `multipart/byteranges` (определённого в {{RFC(7233, "5.4.1")}} и используемого в ответах {{Glossary("HTTP")}} {{HTTPStatus(206)}} "Partial Content", когда запрашиваемые данные возвращаются по частям в нескольких сообщениях, как например, при использовании заголовка {{HTTPHeader("Range")}}).

## Важные для Web-разработчиков MIME типы

### application/octet-stream

Этот тип является базовым для бинарных данных. В связи с тем, что он подразумевает _неопределённые бинарные_ данные, браузеры, как правило, не будут пытаться его обработать каким-либо образом, а вызовут для него диалоговое окно «Сохранить как», как если бы заголовок ответа {{HTTPHeader("Content-Disposition")}} имел значение `attachment`.

### text/plain

Этот тип является базовым для текстовых файлов. Несмотря на то, что он означает "неопределённые текстовые данные", браузеры всё равно могут его отображать.

> **Примечание:** `text/plain` не означает "любой вид текстовых данных". Если браузер ожидает получения какого-то конкретного типа текстовых данных, то с большой вероятностью он не будет считать `text/plain` подходящим типом. Например, при загрузке `text/plain` документа через {{HTMLElement("link")}} элемент, браузер не будет его признавать правильным CSS файлом и использовать для применения стилей. Только `text/css` тип должен использоваться для загрузки CSS документов.

### text/css

CSS документы, используемые для стилизации web-страниц **должны** отправляться, как `text/css` тип. Большинство браузеров не смогут распознавать CSS документы, загруженные с отличным от `text/css` MIME типом.

### text/html

Все HTML данные должны пересылаться с данным типом. Альтернативные MIME типы для XHTML (например, `application/xhtml+xml`) почти не используются в настоящее время.

> [!NOTE]
> Используйте `application/xml` или `application/xhtml+xml`, когда вам необходим строгий синтаксический анализ документов, разделы [`<![CDATA[…]]>`](/ru/docs/Web/API/CDATASection) или элементы, не принадлежащие к пространствам имён HTML/SVG/MathML.

### text/javascript

Согласно HTML спецификации: при пересылке JavaScript файлов, всегда должен использоваться MIME тип `text/javascript`.

По исторически сложившимся причинам, [MIME Sniffing Standard](https://mimesniff.spec.whatwg.org/) (стандарт, определяющий, как браузеры должны интерпретировать медиа типы и выяснять, как обрабатывать данные при неправильно заданных медиа типах) позволяет серверам отправлять JavaScript документы, используя один из нижеперечисленных типов:

- `application/javascript`
- `application/ecmascript`
- `application/x-ecmascript` {{Non-standard_Inline}}
- `application/x-javascript` {{Non-standard_Inline}}
- `text/javascript`
- `text/ecmascript`
- `text/javascript1.0` {{Non-standard_Inline}}
- `text/javascript1.1` {{Non-standard_Inline}}
- `text/javascript1.2` {{Non-standard_Inline}}
- `text/javascript1.3` {{Non-standard_Inline}}
- `text/javascript1.4` {{Non-standard_Inline}}
- `text/javascript1.5` {{Non-standard_Inline}}
- `text/jscript` {{Non-standard_Inline}}
- `text/livescript` {{Non-standard_Inline}}
- `text/x-ecmascript` {{Non-standard_Inline}}
- `text/x-javascript` {{Non-standard_Inline}}

> [!NOTE]
> Несмотря на то, что некоторые {{Glossary("user agent", "пользовательские агенты")}} могут поддерживать какие-то из вышеперечисленных типов, следует всегда должны использовать `text/javascript`. Это единственный MIME-тип, который гарантированно будет работать в настоящее время и в будущем.

Иногда вы можете заметить использование `text/javascript` MIME типа в связке с параметром `charset`, для уточнения кодировки, в которой был написан файл. Такое определение MIME типа является неправильным, и в большинстве случаев браузеры не станут загружать скрипт, передаваемый с таким типом.

### Типы изображений

Файлы, MIME типом которых является `image`, содержат в себе данные изображений. Подтип определяет, какой конкретный формат изображения представлен в данных.

Лишь несколько [типов изображений](/ru/docs/Web/Media/Formats/Image_types) достаточно распространены, чтобы безопасно использоваться на веб-страницах.

### Аудио и видео типы

Так же как в случае с изображениями, стандарт HTML не обязывает браузеры поддерживать какие-либо определённые форматы и кодеки для {{HTMLElement("audio")}} и {{HTMLElement("video")}} элементов, так что при их выборе, важно брать в расчёт целевую аудиторию и диапазон браузеров (а так же версии этих браузеров), которые она может использовать.

Наше [руководство по медиа форматам](/ru/docs/Web/Media/Formats/Containers) предоставляет список общепринятых типов, включая информацию об особых случаях при их использовании, их недостатках, совместимости, а так же других деталях.

Руководства по [аудио](/ru/docs/Web/Media/Formats/Audio_codecs) и [видео](/ru/docs/Web/Media/Formats/Video_codecs) кодекам перечисляют часто поддерживаемые браузерами кодеки, предоставляя детали по их совместимости и техническую информацию, например как много аудио каналов они поддерживают, какой тип сжатия используют, и так далее. Руководство по [используемым в WebRTC кодекам](/ru/docs/Web/Media/Guides/Formats/WebRTC_codecs) развивает эту тему ещё дальше, конкретно описывая кодеки, поддерживаемые популярными браузерами, так чтобы вы могли выбрать кодеки, которые имеют наилучшую поддержку в диапазоне браузеров по вашему выбору.

Что касается MIME типов для аудио и видео файлов, то чаще всего они указывают на формат контейнера (тип файла). Необязательный [параметр `codecs`](/ru/docs/Web/Media/Guides/Formats/codecs_parameter) может быть добавлен к MIME типу для более точного указания, какой кодек и параметры использовались для пересылаемого файла.

Ниже перечислены наиболее часто используемые на веб-страницах MIME типы. Обратите внимание, что это не полный перечень всех доступных типов. Более полный список поддерживаемых форматов может быть найден в [руководстве по медиа форматам](/ru/docs/Web/Media/Formats/Containers).

| MIME тип                                                | Аудио или видео тип                                                                                                                                                                                                                     |
| ------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `audio/wave` `audio/wav` `audio/x-wav` `audio/x-pn-wav` | Аудио файл WAVE формата. С PCM аудио кодеком (WAVE кодек "1"), считающимся наиболее поддерживаемым, а так же другими, имеющими ограниченную поддержку.                                                                                  |
| `audio/webm`                                            | Аудио файл формата WebM. С Vorbis и Opus официально поддерживаемыми WebM спецификацией аудио кодеками.                                                                                                                                  |
| `video/webm`                                            | Видео файл, с возможной аудио дорожкой, формата WebM. С VP8 и VP9, как наиболее распространёнными видео кодеками; Vorbis и Opus, как наиболее распространёнными аудио кодеками.                                                         |
| `audio/ogg`                                             | Аудио файл формата OGG. С Vorbis, как наиболее распространённым аудио кодеком. Хотя на данный момент имеется поддержка и Opus кодека.                                                                                                   |
| `video/ogg`                                             | Видео файл, с возможной аудио дорожкой, в формате OGG. Где Theora – наиболее часто встречающийся видео кодек и Vorbis - наиболее часто встречающийся аудио кодек. Хотя использование кодека Opus становится всё более распространённым. |
| `application/ogg`                                       | Аудио или видео формата OGG. Где Theora – наиболее часто встречающийся видео кодек и Vorbis - наиболее часто встречающийся аудио кодек.                                                                                                 |

### multipart/form-data

`multipart/form-data` тип может быть использован при отправке значений из заполненной [HTML Формы](/ru/docs/Learn_web_development/Extensions/Forms) на сервер.

Как многокомпонентный тип документа, он состоит из различных частей, разделённых специальной границей (строкой, начинающейся с двух чёрточек `--`), где каждая часть представляет собой отдельную сущность и имеет отдельные HTTP заголовки {{HTTPHeader("Content-Disposition")}} и {{HTTPHeader("Content-Type")}} для загружаемых файлов.

```
Content-Type: multipart/form-data; boundary=aBoundaryString
(other headers associated with the multipart document as a whole)

--aBoundaryString
Content-Disposition: form-data; name="myFile"; filename="img.jpg"
Content-Type: image/jpeg

(data)
--aBoundaryString
Content-Disposition: form-data; name="myField"

(data)
--aBoundaryString
(more subparts)
--aBoundaryString--
```

Следующая форма `<form>`:

```html
<form
  action="http://localhost:8000/"
  method="post"
  enctype="multipart/form-data">
  <label>Name: <input name="myTextField" value="Test" /></label>
  <label><input type="checkbox" name="myCheckBox" /> Check</label>
  <label
    >Upload file: <input type="file" name="myFile" value="test.txt"
  /></label>
  <button>Send the file</button>
</form>
```

отправит сообщение:

```
POST / HTTP/1.1
Host: localhost:8000
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
Upgrade-Insecure-Requests: 1
Content-Type: multipart/form-data; boundary=---------------------------8721656041911415653955004498
Content-Length: 465

-----------------------------8721656041911415653955004498
Content-Disposition: form-data; name="myTextField"

Test
-----------------------------8721656041911415653955004498
Content-Disposition: form-data; name="myCheckBox"

on
-----------------------------8721656041911415653955004498
Content-Disposition: form-data; name="myFile"; filename="test.txt"
Content-Type: text/plain

Simple file.
-----------------------------8721656041911415653955004498--
```

### multipart/byteranges

`multipart/byteranges` MIME тип используется для отправки данных в браузер по частям.

При отправке кода состояния {{HTTPStatus("206")}} `Partial Content`, этот MIME тип будет означать, что документ состоит из нескольких частей, по одной для каждого отдельно запрашиваемого диапазона. Аналогично с остальными многокомпонентными типами, заголовок {{HTTPHeader("Content-Type")}} используется для объявления границы `boundary`, разделяющей документ на отдельные компоненты. Каждый компонент имеет заголовок {{HTTPHeader("Content-Type")}}, описывающий тип сегмента данных, и {{HTTPHeader("Content-Range")}}, описывающий его диапазон.

```
HTTP/1.1 206 Partial Content
Accept-Ranges: bytes
Content-Type: multipart/byteranges; boundary=3d6b6a416f9b5
Content-Length: 385

--3d6b6a416f9b5
Content-Type: text/html
Content-Range: bytes 100-200/1270

eta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <meta name="vieport" content
--3d6b6a416f9b5
Content-Type: text/html
Content-Range: bytes 300-400/1270

-color: #f0f0f2;
        margin: 0;
        padding: 0;
        font-family: "Open Sans", "Helvetica
--3d6b6a416f9b5--
```

## **Важность задания правильного** **MIME** **типа**

Большинство серверов отправляет ресурсы неопределённого типа, как `application/octet-stream` MIME тип. Большинство же браузеров, в целях безопасности, не позволяет их никак обрабатывать, вынуждая пользователя сохранять их на жёсткий диск, для дальнейшего использования.

Несколько советов по правильной настройке MIME типов на серверах:

- RAR-сжатые файлы. В этом случае самым правильным вариантом было бы задать тип изначального ресурса; но это не всегда выполнимо, так как .RAR файлы могут хранить в себе несколько типов данных. Тогда, настройте сервер на отправку `application/x-rar-compressed` MIME типа вместе с RAR ресурсами.
- Аудио и видео. Только ресурсы с правильно заданными MIME типами могут производиться в {{HTMLElement("video")}} и {{HTMLElement("audio")}} элементах. Убедитесь, что вы [используете правильные типы для аудио и видео данных](/ru/docs/Web/Media/Formats).
- Запатентованные типы файлов. Избегайте использования `application/octet-stream` при их отправке, так как большинство браузеров не позволит определять способы обработки (например, "Открыть в Word") для этого базового MIME типа. Используйте специальные типы, например `application/vnd.mspowerpoint`, чтобы позволить пользователям открывать загруженный ресурс в программе по их выбору.

## MIME sniffing

В отсутствии заданного MIME типа, или в определённых случаях, когда браузеры полагают, что MIME тип задан неправильно, они могут выполнять _MIME sniffing_ — попытку угадать правильный MIME тип, анализируя характеристики ресурса.

Каждый браузер выполняет MIME sniffing по-своему и при разных условиях (например, Safari будет смотреть на расширение файла, если переданный MIME тип является неподходящим для документа). В этих случаях могут присутствовать опасения по поводу безопасности, так как некоторые MIME типы представляют исполняемые файлы. Сервера имеют возможность предотвращать MIME sniffing, отправляя {{HTTPHeader("X-Content-Type-Options")}} заголовок ответа.

## Другие методы сообщения о типе ресурса

MIME типы не являются единственным способом сообщения типа документа:

- Суффиксы в названиях файлов могут указывать на тип документа, главным образом на Microsoft Windows. Но не все операционные системы могут считать их имеющими смысл (например, Linux или MacOS). А так же нет никакой гарантии, что они будут указывать на правильный тип.
- Магические числа. Синтаксисы различных форматов позволяют узнавать их тип, через анализ их структуры байтов. Например, GIF файлы начинаются с `47 49 46 38 39` шестнадцатеричного значения (`GIF89`), а PNG файлы с `89 50 4E 47` (`.PNG`). Опять же, не все типы документов имеют магические числа, так что этот подход так же не надёжен на 100%.

## Смотрите также

- [Медиа технологии в web](/ru/docs/Web/Media)
- [Руководство по медиа типам и форматам в web](/ru/docs/Web/Media/Formats)
- [Настраивание MIME типов на стороне сервера](/ru/docs/Learn/Server-side/Configuring_server_MIME_types)
