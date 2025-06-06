---
title: Блочный контекст форматирования
slug: Web/CSS/CSS_display/Block_formatting_context
---

{{ CSSRef() }}

## Описание

**Блочный контекст форматирования** — часть механизма отображения веб-страницы в CSS. Это та область, в которой происходит расположение блочных элементов, и в котором плавающие элементы взаимодействуют с другими элементами.

Блочный контекст форматирования создаёт один из следующих способов (методов):

- корневой элемент документа (`<html>`).
- плавающие элементы (элементы, у которых {{ cssxref("float") }} не равно `none`)
- абсолютно позиционированные элементы (элементы, значение {{ cssxref("position") }} которых либо `absolute`, либо `fixed`)
- «строчные блоки» (элементы с {{cssxref("display")}}`: inline-block`)
- ячейки таблицы (элементы с {{ cssxref("display")}}`: table-cell`, являющимся значением по умолчанию для ячеек таблицы в HTML)
- заголовки таблицы (элементы с {{ cssxref("display")}}`: table-caption`, являющимся значением по умолчанию для заголовков таблицы в HTML)
- анонимные ячейки таблицы, неявно создаваемые элементами с {{ cssxref("display") }}`: table`, `table-row`, `table-row-group`, `table-header-group`, `table-footer-group` (значения по умолчанию для таблиц, строк таблиц, «шапок», «подвалов» и тел таблиц в HTML соответственно) либо `inline-table`
- элементы, у которых значение свойства {{ cssxref("overflow") }} отличается от `visible`
- {{ cssxref("display") }}`: flow-root`
- элементы с {{ cssxref("contain") }}`: layout`, `content` или `strict`
- флекс-элементы (непосредственные потомки элемента с {{ cssxref("display") }}`: flex` или `inline-flex`)
- грид-элементы (непосредственные потомки элемента с {{ cssxref("display") }}`: grid` или `inline-grid`)
- многоколоночные контейнеры (элементы, у которых {{ cssxref("column-count") }} или {{ cssxref("column-width") }} не равно `auto`, включая элементы с `column-count: 1`)
- {{ cssxref("column-span") }}`: all` должно всегда создавать новый блочный контекст форматирования, даже если элемент с `column-span: all` не находится в многоколоночном контейнере ([изменение в спецификации](https://github.com/w3c/csswg-drafts/commit/a8634b96900279916bd6c505fda88dda71d8ec51), [баг Chrome](https://bugs.chromium.org/p/chromium/issues/detail?id=709362)).

Блочный контекст форматирования применяется ко всему содержимому того элемента, который его создал.

Блочные контексты форматирования важны для размещения плавающих элементов (см. {{ cssxref("float") }}) и отмены их обтекания (см.{{ cssxref("clear") }}) . Правила размещения плавающих элементов и сброса обтекания применяются только к элементам внутри одного и того же блочного контекста форматирования. Плавающие элементы не влияют на размещение содержимого внутри других блочных контекстов форматирования, и отмена обтекания распространяется только на плавающие элементы из того же самого контекста форматирования. [Схлопывание внешних отступов](/ru/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing) тоже происходит только между блоками из одного и того же блочного контекста форматирования.

## Примеры

### Как сделать плавающему контенту и соседнему с ним контенту одинаковую высоту

Давайте рассмотрим пару примеров, чтобы рассмотреть эффект от создания нового блочного контекста форматирования.

В примере ниже мы имеем плавающий элемент внутри `<div>` с заданным `border`. Содержимое этого `<div>` обтекает плавающий элемент. Так как содержимое `float` выше, чем остальное содержимое, обтекающее его, `border` элемента `div` теперь проходит сквозь `float`. Как объясняется в руководстве [In Flow and Out of Flow](/ru/docs/Web/CSS/CSS_Flow_Layout/In_Flow_and_Out_of_Flow), плавающий элемент был исключён из потока элементов, так что фон и граница `div` включает только его содержимое, но не элемент `float`.

{{EmbedGHLiveSample("css-examples/flow/formatting-contexts/float.html", '100%', 720)}}

### Использование `overflow: auto;`

Создадим новый блочный контекст форматирования, который будет содержать в себе плавающий элемент. Раньше обычным способом сделать это было установить `overflow: auto` или другое значение, отличное от значения по умолчанию `overflow: visible`.

{{EmbedGHLiveSample("css-examples/flow/formatting-contexts/bfc-overflow.html", '100%', 720)}}

Задание `overflow: auto` создало новый блочный контекст форматирования, включающий `float`. Теперь `div` стал мини-слоем внутри нашего слоя. Любые дочерние элементы войдут в него.

Проблема использования `overflow` для создания нового блочного контекста форматирования в том, что свойство `overflow` предназначено для сообщения браузеру как обращаться с переполнением содержимого. Существуют случаи, в которых оно вызовет появление нежелательных скролл-баров или обрезание теней, когда вы используете это свойство только для того, чтобы создать блочный контекст форматирования. Кроме того, оно потенциально делает код менее понятным для следующего разработчика, так как не всегда очевидно, почему использовано `overflow` в данном случае. Если вы используете этот подход, хорошей идеей будет прокомментировать код, чтобы объяснить это.

### Использование `display: flow-root`

Одно из новых значений свойства `display` позволяет нам создавать новый блочный контекст форматирования без всяких потенциально проблемных побочных эффектов. Использование `display: flow-root` как свойство содержащего блока, создаёт новый блочный контекст форматирования.

#### CSS

```html hidden
<div class="box">
  <div class="float">I am a floated box!</div>
  <p>I am content inside the container.</p>
</div>
```

```css
.box {
  background-color: rgb(224, 206, 247);
  border: 5px solid rebeccapurple;
  display: flow-root;
}
.float {
  float: left;
  width: 200px;
  height: 150px;
  background-color: white;
  border: 1px solid black;
  padding: 10px;
}
```

{{EmbedLiveSample("flowroot", 200, 200)}}

С помощью `display: flow-root;` применённом на элементе `<div>`, всё внутри этого контейнера будет участвовать в едином блочном контексте форматирования этого контейнера, и плавающие элементы не будут торчать из нижней части контейнера.

Задание значения `flow-root` имеет смысл тогда, когда вы понимаете, что вы создаёте что-то, что будет действовать так же, как действует корневой `root` элемент (`<html>` в браузерах) в том плане, что он создаёт новый контекст для компоновки потока внутри него.

> **Примечание:** `display: flow-root;` [не поддерживается](https://caniuse.com/#search=flow-root) в Safari.

### Схлопывание границ margin

Создание нового блочного контекста форматирования предотвращает эффект [схлопывания границ](/ru/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing) между двумя соседними div:

#### HTML

```html
<div class="blue"></div>
<div class="red-outer">
  <div class="red-inner">red inner</div>
</div>
```

#### CSS

```css
.blue,
.red-inner {
  height: 50px;
  margin: 10px 0;
}

.blue {
  background: blue;
}

.red-outer {
  overflow: hidden;
  background: red;
}
```

{{EmbedLiveSample("Схлопывание_границ_margin", 120, 120)}}

## Спецификации

- [CSS 2.1](https://www.w3.org/TR/CSS21/visuren.html#q15)
- [CSS Display Level 3](https://drafts.csswg.org/css-display/#block-formatting-context)

## Статьи по теме

- {{ cssxref("float") }}, {{ cssxref("clear") }}
- Ключевые концепции CSS
  - [Синтаксис CSS](/ru/docs/Web/CSS/CSS_syntax/Syntax)
  - [@-правила](/ru/docs/Web/CSS/CSS_syntax/At-rule)
  - [комментарии](/ru/docs/Web/CSS/CSS_syntax/Comments)
  - [специфичность](/ru/docs/Web/CSS/CSS_cascade/Specificity)
  - [наследование](/ru/docs/Web/CSS/CSS_cascade/Inheritance)
  - [блочная модель](/ru/docs/Web/CSS/CSS_box_model/Introduction_to_the_CSS_box_model)
  - [режимы компоновки](/ru/docs/Glossary/Layout_mode)
  - [модели визуального форматирования](/ru/docs/Web/CSS/CSS_display/Visual_formatting_model)
  - [Схлопывание отступов](/ru/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing)
  - Значения
    - [начальные](/ru/docs/conflicting/Web/CSS/CSS_cascade/Value_processing)
    - [вычисленные](/ru/docs/conflicting/Web/CSS/CSS_cascade/Value_processing_e3410028f0a698ddd9f74225ea8d122c0a582707d683fdd173e681e62003518d)
    - [используемые](/ru/docs/conflicting/Web/CSS/CSS_cascade/Value_processing_67ecc2d1089286b6003d201c901ee7218b8f627858ae89823dc40509095cd65b)
    - [действительные](/ru/docs/Web/CSS/CSS_cascade/Value_processing)
  - [Синтаксис определения значений](/ru/docs/Web/CSS/Value_definition_syntax)
  - [Сокращённые свойства](/ru/docs/Web/CSS/CSS_cascade/Shorthand_properties)
  - [Замещаемые элементы](/ru/docs/Web/CSS/CSS_images/Replaced_element_properties)
