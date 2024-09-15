# normalize.scss
normalize.scss
/**
  Нормализация блочной модели
 */
*,
::before,
::after {
	box-sizing: border-box;
}

/**
	Убираем внутренние отступы слева тегам списков,
	у которых есть атрибут class
  */
:where(ul, ol):where([class]) {
	padding-left: 0;
}

/**
	Убираем внешние отступы body и двум другим тегам,
	у которых есть атрибут class
  */
body,
:where(blockquote, figure):where([class]) {
	margin: 0;
}

/**
	Убираем внешние отступы вертикали нужным тегам,
	у которых есть атрибут class
  */
:where(h1, h2, h3, h4, h5, h6, p, ul, ol, dl):where([class]) {
	margin-block: 0;
}

:where(dd[class]) {
	margin-left: 0;
}

:where(fieldset[class]) {
	margin-left: 0;
	padding: 0;
	border: none;
}

/**
	Убираем стандартный маркер маркированному списку,
	у которого есть атрибут class
  */
:where(ul[class]) {
	list-style: none;
}

:where(address[class]) {
	font-style: normal;
}

/**
	Обнуляем вертикальные внешние отступы параграфа,
	объявляем локальную переменную для внешнего отступа вниз,
	чтобы избежать взаимодействие с более сложным селектором
  */
p {
	--paragraphMarginBottom: 24px;

	margin-block: 0;
}

/**
	Внешний отступ вниз для параграфа без атрибута class,
	который расположен не последним среди своих соседних элементов
  */
p:where(:not([class]):not(:last-child)) {
	margin-bottom: var(--paragraphMarginBottom);
}

/**
	Упрощаем работу с изображениями
  */
img {
	display: block;
	max-width: 100%;
}

/**
	Наследуем свойства шрифт для полей ввода
  */
input,
textarea,
select,
button {
	font: inherit;
}

html {
	/**
	  Пригодится в большинстве ситуаций
	  (когда, например, нужно будет "прижать" футер к низу сайта)
	 */
	height: 100%;
}

/**
	Плавный скролл
  */
html,
:has(:target) {
	scroll-behavior: smooth;
}

body {
	/**
	  Пригодится в большинстве ситуаций
	  (когда, например, нужно будет "прижать" футер к низу сайта)
	 */
	min-height: 100%;
	/**
	  Унифицированный интерлиньяж
	 */
	line-height: 1.5;
}

/**
	Приводим к единому цвету svg-элементы
  */
svg *[fill] {
	fill: currentColor;
}
svg *[stroke] {
	stroke: currentColor;
}

/**
	Чиним баг задержки смены цвета при взаимодействии с svg-элементами
  */
svg * {
	transition-property: fill, stroke;
}

/**
	Удаляем все анимации и переходы для людей,
	которые предпочитают их не использовать
  */
@media (prefers-reduced-motion: reduce) {
	*,
	::before,
	::after {
		animation-duration: 0.01ms !important;
		animation-iteration-count: 1 !important;
		transition-duration: 0.01ms !important;
		scroll-behavior: auto !important;
	}
}
