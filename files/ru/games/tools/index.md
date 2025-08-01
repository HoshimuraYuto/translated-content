---
title: Инструменты для разработки игр
slug: Games/Tools
---

На этой странице вы можете найти ссылки на наши статьи по инструментам для разработки игр, которая в конечном итоге нацелена на покрытие фреймворков, компиляторов и инструментов отладки.

- [asm.js](/ru/docs/Games/Tools/asm.js)
  - : asm.js это очень ограниченное подмножество языка JavaScript, которое можно значительно оптимизировать и запустить в опережающем времени (AOT), компилируя движок гораздо быстрее, чем при типичной производительности языка. А это, конечно же, замечательно для игр.
- [Emscripten](https://github.com/kripken/emscripten/wiki)
  - : Низкоуровневая виртуальная машина(LLVM) для JavaScript; с Emscripten вы можете компилировать C++ и другие языки, которые можно копировать в байт-код LLVM с высокой производительностью JavaScript. Это отличный веб-инструмент! Вот [полезный туториал по Emscripten](https://github.com/kripken/emscripten/wiki/Tutorial), доступный на вики. Заметьте, что мы [стремимся охватить Emscripten в своих разделах на MDN](/ru/docs/Emscripten).
- [Gecko profiler](https://addons.mozilla.org/en-us/firefox/addon/gecko-profiler/)
  - : Gecko profiler позволяет профилировать код, чтобы понять, где имеются проблемы производительности, и добиться максимальной скорости в .
- [Игровые движки и инструменты](/ru/docs/Games/Tools/Engines_and_tools)
  - : Список движков, шаблонов и технологий, полезных для разработчиков.
- [Shumway](/ru/docs/Mozilla/Projects/Shumway)
  - : Shumway это рендер для Adobe Flash построенный полностью на JavaScript, WebGL, etc., преодолевающий разрыв между Flash и web-стандартами. Это статья поясняет, как пользоваться Shumway,и как вносить исправления в проекте.
- Инструментарий для разработки и отладки игр
  - : Чем это отличается от обычной отладки веб-приложения? Какие специальные инструменты доступны? Многое из этого доступно в [инструментах](https://firefox-source-docs.mozilla.org/devtools-user/index.html), но здесь мы должны обеспечить своего рода практический учебник для отладки игры, с ссылками :
    - Обзор базовых инструментов
    - [Редактор шейдеров](https://firefox-source-docs.mozilla.org/devtools-user/shader_editor/index.html)
    - Производственные инструменты (все ещё находятся в производстве, по оценкам, в начале 2014 года)
