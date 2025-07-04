# Как техать в VS Code на macOS
Этот файл во многом полагается на старый [гайд](https://telegra.ph/V-chyom-tehat-06-28), но дополняет его для пользователей macOS.

Опять же, как и предыдущий гайд, он не рассчитан на обучение тому, как техать, а тому, как использовать VS Code как локальную замену Overleaf, так как он обладает рядом **преимуществ**:
- моментальная сборка при сохранении
- быстрая проверка грамматики
- возможность использования copilot
- inline калькулятор python
- независимость от сбоящих серверов Overleaf

Но, очевидно, есть и минус в виде невозможности совместного редактирования. В таком случае, проще копировать при надобности документ в overleaf, а затем его заново выгружать.

Итак, перейдем к гайду.

## Как установить LaTeX в macOS

- Установить VS Code.
- Установить [MacTex с официального сайта](https://tug.org/mactex/mactex-download.html).
- Установить расширение [LaTex Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)

*Все остальные зависимости устанавливаются автоматически*

После этого вы сможете сразу открыть свой первый документ через:
- ``⌥ + ⌘ + B`` - скомпилировать .tex файл (Вы должны находиться в файле с форматом .tex)
- ``⌥ + ⌘ + V`` - открыть скомпилированный .pdf файл

Я рекомендую сразу поменять шорткат открытия документа, так как с существующим легко сломать пальцы. Делается это через:
- ``shift + ⌘ + P`` → ``Preferences: Open Keyboard Shortcuts``.
- В поиске ищем ``LaTeX Workshop: View LaTeX PDF file``.
- Дважды нажимаем и меняем комбинацию. Я, например, использую ``shift + ⌘ + V``.

## Как упростить себе жизнь
Выше было описано только базовые моменты, которых в целом, должно хватить, но я советую продолжить улучшать пользовательский опыт для самих себя.

### Автопереход по документу
Одна из киллерфич Overleaf автоматический переход к коду при нажатии на фрагмент в .pdf файле. Но это же есть при установке в LaTex WorkShop. Для этого всего лишь надо нажать на текст с зажатой клавишей **cmd** (⌘).
### Как вставлять изображения
В Overleaf вы можете вставлять изображения, и они сами добавятся в документ, как это сделать в VS Code?

- Скачайте [расширение Paste Image](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image)
- Настройте его для работы с TeX:
    - Откройте настройки: ``shift + ⌘ + P`` → ``Preferences: Open User Settings (JSON)``
    - Вставьте следующее:
        ```json
        "pasteImage.insertPattern": "\\begin{figure}[h]\n  \\centering\n  \\includegraphics[width=0.5\\textwidth]{files/${imageFileName}}\n  \\caption{}\n  \\label{fig:${imageFileName}}\n\\end{figure}",
        "pasteImage.filePathConfirmInputBoxMode": "onlyName",
        "pasteImage.encodePath": "none",
        "pasteImage.basePath": "${currentFileDir}",
        "pasteImage.showFilePathConfirmInputBox": true,
        "pasteImage.defaultName": "${currentFileNameWithoutExt}-HH-mm-ss",
        "pasteImage.path": "${currentFileDir}/files",
        ```
    Так как вставка изображения и открытие документа находятся на одном шорткате ``⌥ + ⌘ + V``, вам понадобится его поменять, если вы этого еще не сделали:
    - ``shift + ⌘ + P`` → ``Preferences: Open Keyboard Shortcuts``
    - В поиске ищем ``Paste Image``.
    - Дважды нажимаем и меняем комбинацию. Я, например, использую ``ctrl + V``.

После этого вы можете открыть .tex файл и вставить изображение из буфера выбранной комбинацией.
> При вставке сверху должно появиться поле ввода названия. Заметьте его!)

### Автокомпиляция
Лично мне лень каждый раз нажимать отдельную комбинацию для компиляции файла, поэтому для автоматической компиляции при сохранении можно сделать следующее:

- Откройте настройки: ``shift + ⌘ + P`` -> ``Preferences: Open User Settings (JSON)``
- Вставьте следующее:
    ```json
        "latex-workshop.latex.autoBuild.run": "onSave",
        "latex-workshop.latex.autoBuild.cleanAndRetry.enabled": true,
        "latex-workshop.latex.autoClean.run": "onBuilt"
    ```

Теперь при сохранении файла ``⌘ + S`` файл будет автоматически перекомпилироваться и сразу изменяться в превью.

### Проверка грамматики
Для проверки грамматики и спеллинга (все, что сложнее, умеет обрабатывать **ТОЛЬКО** word) можно использовать [расширение LTeX](https://marketplace.visualstudio.com/items?itemName=valentjn.vscode-ltex).

Для отображения ошибок прямо в коде можно использовать [Error Lens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens).

Быстро исправлять ошибки можно выставив каретку на ошибку и нажав ``shift + ⌘ + 7``.

Если вам не нравится такая агрессивная проверка, можете использовать [расширение Code Spell Checher](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) с [дополнением для русского языка](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker-russian). Другие языки устанавливаются так же.

### GitHub Copilot
Самое главное преимущество VSCode перед OverLeaf является наличие Github Copilot. Более того, каждому студенту его можно получить бесплатно через [github edu](https://github.com/education).

Я крайне осуждаю использование дегенеративных сетей для решения задач, но приведу ниже несколько кейсов, при которых использование copilot очень удобно.

Вызвать строку ввода запроса можно через комбинацию ``⌘ + I`` прямо в документе, после этого вам откроется мир полной автоматизации:
- Попросите переписать формулу из изображения в буфере в LaTeX формулу.
- Попросите перенести данные в таблицу.
- Проверьте пунктуацию и структуру текста.
- Быстро починить ошибки и что-то добавить, например, оглавление.

В общем, Copilot открывает огромные возможности для быстрого редактирования .tex документов, что особенно спасает, если вы не особо знакомы с языком разметки.

## Заключение
Возможно, я буду дополнять этот гайд, но пока это все, чем я хотел поделиться. Надеюсь, он пригодится вам, чтобы порадовать ассистентов или кого-нибудь ещё красивым домашним заданием.