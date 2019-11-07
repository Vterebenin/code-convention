# CODE convention
Данное соглашение разъясняет рекомендаци и правила по написанию кода, предполагающего масштабируемые приложений.

**Table of Contents**

[TOC]


# Css
### Именование классов
Если необходимо какому либо компоненту дать класс, нужно исходить из соображений конвенции [БЭМ](https://ru.bem.info/methodology/quick-start/ "БЭМ").
На практике это выглядит так:
Есть абстрактный компонент хлебных крошек.
Шаблон этого компонента может выглядеть так: 

```html
<template>
  <ul>
    <li>Главная</li>
    <li>Каталог</li>
    <li>Канцтовары</li>
    <li>Письменная ручка</li>
  </ul>
</template>
```
Допустим у нас стоит задача задать стили для ul(например, убрать отступы), для li(например, добавить у каждого пунка меню after-контент), а айтем "канцтовары" сделать красным цветом. 
префикс либо b, либо какой-то что-то абстрактное(для ак ксуф сейчас префикс af)
Весь список это отдельный блок(состоит из префикса и названия блока). каждый элемент списка будет являться отдельным элементом. Так как третьему элементу нужен особый стиль, у него будет модификатор.
Нейминг для классов будет таков: 
```html
<template>
  <ul class="b-breadcrumbs">
    <li class="breadcrumbs__item">Главная</li>
    <li class="breadcrumbs__item">Каталог</li>
    <li class="breadcrumbs__item breadcrumbs__item--red">Канцтовары</li>
    <li class="breadcrumbs__item">Письменная ручка</li>
  </ul>
</template>
```
scss же будет выглядеть примерно вот так: 
```scss
.b-{
  &breadcrumbs {
    /* стили для ul */
    .breadcrumbs__item {
      /* стили для li */
      &--red {
	/* стили для li{канцтовары} */
      }
    }
  }
}
```

***Вы должны чувствовать себя негодяем, если вы:***
- пишите стили, используя ключевое слово !important
- используете большую(>2) вложенность селекторов
- используете css хаки вроде регулярок или переопределения повторением классов
- без необходимости пользуетесь nth-child, селекторами + и ~(и тд)

Эти вещи затрудняют переиспользование и размывают границы для блоков, которые вы стилизуете, а некоторые даже замедляют быстродействие приложений. Без острой необходимости избегайте вещей описанных выше. 

**P.S.** бэм и vuetify плохо дружат. Иногда злобный мистер vuetify подкладывает нам свинью в виде селекторов а-ля .v-icon.v-icon. В связи с этим, какие-то хаки понадобятся, главное знайте меру или умело обходите эту проблему.

# Именование
|  Абстрактная единица |  стиль наименования  |
| ------------ | ------------ |
|  css классы  |  кебаб-кейсы  |
|  vue-компоненты внутри template |  кебаб-кейсы  |
|  наименование компонентов |  КамелКейсы  |
|  Функции |  камелКейсы  |
|  Переменные |  камелКейсы  |
|  TBD |  TBD  |

# Порядок частей компонента во vuetify
### TBD

# Именование коммитов
Строгих правил нет, но есть идеи: 
именовать коммиты в третьем лице:
1) Допустим, вы переименовали функцию sayMy(name) в logThis(string) в компоненте SayMyName.vue. Что **сделал** этот коммит? Этот коммит ***переименовал функцию в компоненте SayMyName***. Так и пишите в коммите:
> **git commit -m "переименовал функцию в компоненте SayMyName"**

То есть старайтесь думать о коммитах как "Этот коммит сделал что-то", где "сделал что-то" имя для коммиста.

2) Избегайте союза "и" в коммитах. В идеале его вообще быть не должно. Каждый коммит должен быть отдельной логической единицей.

*Неправильно писать:*

git commit -m "убирал отступы у логотипа и добавил новые зависимости"
git commit -m "убил оленя; порубил дрова"

*Правильно: *

git commit -m "убил оленя"
git commit -m "порубил дрова"

Так же в начале каждого коммита желательно ставить префикс действия
|  префикс |  когда ставить  |
| -------- | --------------- |
|  feat  |  при внедрении новой особенности  |
|  fix |  при баг фиксах  |
|  ref |  при рефакторинге  |
|  doc |  при документировании  |

так же нужно определиться с языком(en-ru?).
