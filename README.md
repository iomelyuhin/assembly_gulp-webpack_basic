# SITE_NAME

Перед установкой зависимостей и запуском проекта убедитесь, что у вас установлена [последняя версия Node.js & NPM](https://nodejs.org/en/download/current/), а так же [последняя версия Yarn](https://yarnpkg.com/ru/docs/install) 

##  Чтобы развернуть проект необходимо:
```sh
$ git clone https://github.com/iomelyuhin/ActualKeylogger.git .
$ yarn
```
или
```sh
$ npm install
```

## Скрипты package.json:


gulp - Запустит developer-mode с горячей перезагрузкой и соберет проект в dist


#### Чтобы запустить скрипт:
```sh
$ npm run имя_скрипта
```
или
```sh
$ yarn имя_скрипта
```
## Что где лежит
| Путь | Назначение |
| ------ | ------ |
| src/ | Рабочая папка проекта |
| dist/ | Собранный проект |
| gulpfile.js | Конфиг Gulp |
| webpack.config.js | Конфиг Webpack (для сборки JS) |
| postcss.config.js | Конфиг PostCss (для сборки CSS) |
| src/views | Разметка на Pug (Jade) |
| src/views/pages | Страницы проекта |
| src/views/common | Компоненты страниц |
| src/views/main.layout.pug | Шаблон главной


## Как создать новую страницу?
#### 1. Создаём файл .pug в папке src/views/pages
#### 2. В первой строчке подключаем шаблон страницы
```sh
extends ../main.layout.pug
```
#### 3. Меняем title страницы:
```sh
block variables
  - var title = 'Блог'
```
#### 4. Создаём содержимое страницы:
```sh
block content
  h1 "Блог"
```
#### 5. Подключаем скрипты к странице(добавить .bundle перед .js):
```sh
block scripts
  script(src='assets/scripts/works.bundle.js')
```
#### 6. Подключаем компоненты в содержимое страницы:
```sh
  h1 "Мои работы"
  include ../common/slider.pug
```

## Как создать новый скрипт и подключить его?

#### 1. Создаём файл [pageName].js в папке src/assets/scripts/
#### 2. Подключаем на странице:
```sh
block scripts
  script(src='assets/scripts/works.bundle.js')
```
#### 3. Добавляем правило сборщику:

##### - идём в файл webpack.config.js
##### - находим там entry{} на 5 строке
##### - добавляем строку с описанием своего файла по аналогии:
```sh
[pageName]: "./src/assets/scripts/[pageName].js"
```
#### 4. Подключаем модули:
##### - Создаём файл модуля в src/assets/modules/[moduleName].js
##### - Инициализируем в нем функцию и экспортируем её:
```sh
function sliderInit() {
  //code here
};
module.exports = sliderInit;
```
##### - в [pageName].js импортируем и вызываем наш модуль:
```sh
import slider from "./modules/slider"

slider();
```