---
title: text-indent
slug: Web/CSS/text-indent
---

{{CSSRef}}

La propriété **`text-indent`** définit la longueur qui doit être laissée avant le début de la première ligne d'un élément contenant du texte.

L'espacement horizontal se fait en accord avec la bord gauche (ou droit pour les dispositions de droite à gauche) de l'élément contenant le texte. Par défaut, cela ne contrôle que l'indentation de la première ligne du bloc mais les mots-clés `hanging` et `each-line` peuvent être utilisés pour modifier ce comportement.

{{InteractiveExample("CSS Demo: text-indent")}}

```css interactive-example-choice
text-indent: 0;
```

```css interactive-example-choice
text-indent: 30%;
```

```css interactive-example-choice
text-indent: -3em;
```

```css interactive-example-choice
text-indent: 3em each-line;
```

```css interactive-example-choice
text-indent: 3em hanging;
```

```css interactive-example-choice
text-indent: 3em hanging each-line;
```

```html interactive-example
<section id="default-example">
  <div id="example-element">
    <p>
      This text is contained within a single paragraph. This paragraph is two
      sentences long.
    </p>
    <p>
      This is a new paragraph. There is a line break element
      <code>&lt;br&gt;</code> after this sentence.<br />There it is! Notice how
      it affects the indentation.
    </p>
  </div>
</section>
```

```css interactive-example
section {
  font-size: 1.25em;
  background-color: #483d8b;
  align-items: start;
}

#example-element {
  text-align: left;
  margin: 0 0 0 3em;
  background-color: #6a5acd;
  color: white;
}
```

## Syntaxe

```css
/* Valeurs de longueur */
/* Type <length>       */
text-indent: 3mm;
text-indent: 40px;

/* Valeurs de pourcentages */
/* relatives à la largeur  */
/* du bloc englobant       */
/* Type <percentage>       */
text-indent: 15%;

/* Valeurs avec un mot-clé */
text-indent: 5em each-line;
text-indent: 5em hanging;
text-indent: 5em hanging each-line;

/* Valeurs globales */
text-indent: inherit;
text-indent: initial;
text-indent: unset;
```

### Valeurs

- `<length>`
  - : L'indentation est définie de façon absolue avec une longueur ({{cssxref("&lt;length&gt;")}}). On peut utiliser des valeurs négatives. Voir la page sur {{cssxref("&lt;length&gt;")}} pour les différentes unités possibles.
- `<percentage>`
  - : L'indentation est définie en proportion de la largeur du bloc englobant (type {{cssxref("&lt;percentage&gt;")}}).
- `each-line` {{experimental_inline}}
  - : L'indentation n'affecte que la première ligne du bloc et chaque ligne située après un saut de ligne forcé. Cela n'affecte pas les lignes situées après un retour à la ligne automatique (_wrap_).
- `hanging` {{experimental_inline}}
  - : Inverse les lignes indentées. Toutes les lignes, sauf la première, seront indentées.

## Définition formelle

{{CSSInfo}}

## Syntaxe formelle

{{CSSSyntax}}

## Exemples

### Indentation simple

#### HTML

```html
<p>
  Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy
  nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
</p>
<p>
  Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy
  nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
</p>
```

#### CSS

```css
p {
  text-indent: 5em;
  background: powderblue;
}
```

### Résultat

{{EmbedLiveSample('Indentation_simple','100%','100%') }}

### Indentation proportionnelle

#### HTML

```html
<p>
  Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy
  nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
</p>
<p>
  Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy
  nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
</p>
```

#### CSS

```css
p {
  text-indent: 30%;
  background: plum;
}
```

#### Résultat

{{EmbedLiveSample('Indentation_proportionnelle','100%','100%')}}

## Spécifications

{{Specifications}}

## Compatibilité des navigateurs

{{Compat}}
