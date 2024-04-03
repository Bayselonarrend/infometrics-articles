# ![image](https://github.com/Bayselonarrend/infometrics-articles/assets/105596284/ef7e8987-3f98-4e2f-a9a6-1d112ff72f79) infostart-articles
Автоматическое обновление списка последних статей Инфостарт для Readme профиля. Реализовано при помощи Github Actions

## Как добавить себе?

1. В файл Readme добавить блок следующего вида. Этот блок всегда должен быть пустой - при обновлении статей он будет затираться.
 
 ```html
 <div id="infostart_posts">

 </div>
 ```
   
2. Создать новый Action в репозитории профиля. Пример yml файла ниже

## Пример yml файла

```yml
name: Infostat
on:
  schedule: [{cron: "0 0 * * *"}] # Расписание выполнения. В данном примере - каждый день в 0.00
  workflow_dispatch:
jobs:
  Update:
    runs-on: ubuntu-latest 
    permissions:
        contents: write
    steps:

      - uses: bayselonarrend/infometrics-articles@1.0
        with:
          profile-id: '1793672'                 # ID профиля Infostart
          count: '3'                            # Количество выводимых статей. По умолчанию - 3
          readme-file: './README.md'            # Путь к Readme файлу. По умолчанию - ./README.md (Регистр важен!)

```
## О составе проекта

В основе данного Action лежит скрипт на OneScript - вы легко можете доработать его под свои нужды, если вам так захочется. 
Шаблон вывода разметки для Readme тоже находится там.
