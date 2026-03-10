# Начало работы с Tailwind
Мой самописный гайд

## Установка
[Официальный гайд по установке `Tailwind`](https://tailwindcss.com/docs/installation/tailwind-cli)

Чтобы установить Tailwind нужно сначала определиться с тем через что устанавливать. 

Есть 5 различных вариантов:
1. [`Using Vite`](https://tailwindcss.com/docs/installation/using-vite)
2. [`Using PostCSS`](https://tailwindcss.com/docs/installation/using-postcss)
3. [`Tailwind CLI`](https://tailwindcss.com/docs/installation/tailwind-cli) (текущий вариант)
4. [`Framework Guides`](https://tailwindcss.com/docs/installation/framework-guides)
5. [`Play CDN`](https://tailwindcss.com/docs/installation/play-cdn)

В данном проекте я решил выбрать вариант через [`Tailwind CLI`](https://tailwindcss.com/docs/installation/tailwind-cli).

### Шаги установки
0. Предварительная подготовка:
    
    - Для дальнейшей работы понадобится установленная [`Node`](https://nodejs.org)
    - Все команды, показанные в этом гайде, для терминала [`bash`](https://ru.wikipedia.org/wiki/Bash)

1. Установить `Tailwind CSS`:

    Установить `tailwindcss` и `@tailwindcss/cli` через npm.
    ```bash
    npm install tailwindcss @tailwindcss/cli
    ```

2. Импорт `Tailwind` в основной CSS файл:

    2.1. Создаём основной `.css` файл 
    (в этом проекте это `./css/styles.css`)

    2.2. В созданном `.css` файле импортируем `Tailwind`
    ```css
    @import "tailwindcss";
    ```

3. Инициализация `Tailwind` в проекте:

    ```bash
    npx @tailwindcss/cli -i [относительный путь до основного `.css` файла] -o [относительный путь для создания файла билда `.css` `Tailwind`] --watch
    ```

    В данном проекте команда была такой:

    ```bash
    npx @tailwindcss/cli -i ./css/styles.css -o ./css/dist.css --watch
    ```

    Пояснения:

    - `npx` - Утилита из среды Node.js для работы с пакетами. Загружает (если не загружен) и запускает пакет.

    - `@tailwindcss/cli` - Инструмент пакета @tailwindcss. `cli` расшифровывается как `Command Line Interface` (интерфейс командной строки). Сканирует `.html` и понимает какие стили нужно создать.

    - `-i` (input) - Флаг для указания пути к основному `.css` файлу, где находится 
        ```css 
        @import "tailwindcss";
        ```
        откуда `Tailwind` берёт инструкции.

    - `-o` (output) - Флаг для указания пути сохранения сгенерированного кода (билда) `.css`. Именно этот файл нужно подключать в `.html`. 

    - `--watch` - Флаг режима наблюдения. Нужен чтобы команда не выполнилась и завершилась, а следила за сохранениями файлов `.html` и обновляла в реальном времени файл билда `.css`.

4. Подключаем скомпилированный файл билда `.css` к `.html`:

    В файле `.html` в теге `<head>...</head>` пишем
    ```html
    <link href="[Путь до файла билда]" rel="stylesheet">
    ``` 
    В этом проекте это выглядит так:
    ```html
    <!doctype html>
    <html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>HP-Education-TailwindCss</title>

        <link href="./css/dist.css" rel="stylesheet"> <!-- Строка подключения -->
    </head>
    <body>
        ...
    </body>
    </html>
    ``` 
    После этого можно спокойно работать над проектом используя `Tailwind`

5. Подключение скрипта к `package.json` (Доп)

    Когда проектов станет много, вводить руками 
    ```bash
    npx @tailwindcss/cli...
    ``` 
    станет лень. Разработчики обычно создают файл `./package.json` (если его нет) и прописывают команду туда.

    ```json
    {
        "scripts": {
            "dev": "npx @tailwindcss/cli -i [относительный путь до основного .css файла] -o [относительный путь для создания файла билда .css] --watch"
        },
        ...
    }
    ```

    В этом проекте файл `./package.json` выглядит так:
    ```json
    {
        "scripts": {
            "dev": "npx @tailwindcss/cli -i ./css/styles.css -o ./css/dist.css --watch"
        },
        "dependencies": {
            "@tailwindcss/cli": "^4.2.1",
            "tailwindcss": "^4.2.1"
        }
    }
    ```

    Теперь для запуска достаточно ввести в терминале:
    ```bash
    npm run dev
    ```

### Советы

- Не редактируйте файл сборки (в этом проекте это `./css/dist.css`), так как он перезаписывается при каждом сохранении
- Если используете `Git`, то в файл `.gitignore` следует добавить:
    - Папку `./node_modules`
    - файл билда (в данном случае `./css/dist.css`)