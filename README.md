# ![image](https://github.com/Bayselonarrend/infometrics-articles/assets/105596284/ef7e8987-3f98-4e2f-a9a6-1d112ff72f79) infometrics-articles
Автоматическое обновление списка публикаций Инфостарт для Readme профиля. Реализовано при помощи Github Actions.

Это пока предрелиз - в нем могут быть баги. Он был проверен на ~20 профилей из топа Инфостарта, но все равно:<br>
а) Рекомендуется сначала попробовать не в профиле, а в приватном репозитории<br>
б) Будет очень хорошо, если при нахождении бага вы напишите в Issues<br>
<br>

## Как добавить себе?

1. В файл Readme добавить блок следующего вида. Этот блок всегда должен быть пустой - при обновлении публикаций он будет затираться.
 
 ```html
 <div id="infostart_posts">

 </div>
 ```
   
2. Создать новый Action в репозитории профиля. Пример yml файла ниже

```yml
name: Infostart
on:
  schedule: [{cron: "0 0 * * *"}] # Расписание выполнения. В данном примере - каждый день в 0.00
  workflow_dispatch:
jobs:
  Update:
    runs-on: ubuntu-latest 
    permissions:
        contents: write
    steps:

      - uses: bayselonarrend/infometrics-articles@1.2
        with:
          profile-id: '1793672'                 # ID профиля Infostart
          count: '3'                            # Количество выводимых публикаций. Необязательно, по умолчанию - 3, Максимум - 10
          readme-file: './README.md'            # Путь к Readme файлу. Необязательно, по умолчанию - ./README.md (Регистр важен!)
```

3. Готово, можно запустить вручную Action

<br>

## Пример вывода публикации в Readme

> <img src="https://infostart.ru/upload/iblock/e1e/e1eddd228630c7c47b98a2baa0f48430.png?a6374f47-0a23-4bb8-ad1c-e48b0a8608de" width="96" align="left"> 
> <h4 style="color: white;"><a href="https://infostart.ru/1c/articles/2068854/">Особенности национального Workflow: Github Actions и OneScript</a></h4>
> <small>Сегодня мы посмотрим на Github Actions - встроенный инструментарий Github для автоматизации рабочих процессов. Разберем, что это такое, зачем и причем тут OneScript.</small>  
> <br clear="left">
>
> | :star: +37 |  :calendar: 25.03.2024 |  :speech_balloon: 3 |  :eyes: 1393 |
>  |-|-|-|-|  

## Дополнительные возможности

### Шаблоны вывода публикаций

Для вывода публикаций используется текстовый шаблон по умолчанию, но вы можете использовать и свой. Для использования своего шаблона необходимо:

1. Создать любой текстовый файл, где будет хранится шаблон. В нем могут содержаться следующие параметры:
    -  %1 - URL изображения
    -  %2 - Заголовок публикации
    -  %3 - Ссылка на публикацию
    -  %4 - Число звезд
    -  %5 - Описание публикации
    -  %6 - Дата публикации
    -  %7 - Комментарии
    -  %8 - Просмотры

  Например, шаблон по умолчанию
  
  ```html
  > <img src="%1" width="96" align="left">
  > <h4 style="color: white;"><a href="%3">%2</a></h4>
  > <small>%5</small>
  > <br clear="left">
  > 
  > | :star: %4 |  :calendar: %6 |  :speech_balloon: %7 |  :eyes: %8 |
  > |-|-|-|-|
  ```
  
  2. Прописать путь к этому файлу в параметр template
  
  ```yml
      - uses: bayselonarrend/infometrics-articles@1.2
        with:
          profile-id: '1793672'
          count: '3'
          readme-file: './README.md'
          template: ./tm.html  # Тут - tm.html в корне репозитория
  ```
<br>


### Фильтр публикаций

По умолчанию в список публикаций выводится лучшие из профиля.

Также можно использовать другие фильтры:

   - 'Top' - Лучшие публикации по звездам
   - 'Download' - Топ-загрузок
   - 'Sale' - Топ-продаж
   - 'Comment' - Топ-комментариев
   - 'Show' -Топ-просмотров
   - '' - Последние

Для этого измените yml файл и параметр filter
  ```yml
      - uses: bayselonarrend/infometrics-articles@1.2
        with:
          profile-id: '1793672'
          count: '3'
          readme-file: './README.md' # Путь к Readme файлу. Необязательно, по умолчанию - ./README.md (Регистр важен!)
          filter: 'Download'         # Какие публикации выводить. Необязательно, по умолчанию - лучшие. Другие варианты: Top - Лучшие, Download - Топ-загрузок, Sale - Топ-продаж, Comment - Топ-комментариев, Show - Топ-просмотров, "" - Последние
  ```
<br>


## О составе проекта

В основе данного Action лежит скрипт на OneScript - вы легко можете доработать его под свои нужды, если вам так захочется.
Шаблон вывода разметки для Readme тоже находится там.
<hr><br>

>![Infostart](https://github.com/Bayselonarrend/TelegramEnterprise/raw/main/infostart.svg)<br>
>Статья на Инфостарте: [Обновляемый список последних статей Инфостарт для профиля Github](https://infostart.ru/1c/articles/2083470/)<br>
