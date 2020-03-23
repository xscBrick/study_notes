<span>  标签
<span> 标签被用来组合文档中的行内元素，以便通过样式来格式化它们。当对它应用样式时，它才会产生视觉上的变化。

```php+HTML
<p><span>some text.</span>some other text.</p>
```



如果不对 span 应用样式，那么 span 元素中的文本与其他文本不会任何视觉上的差异。尽管如此，上例中的 span 元素仍然为 p 元素增加了额外的结构。

可以为 span 应用 id 或 class 属性，这样既可以增加适当的语义，又便于对 span 应用样式。

可以对同一个 <span> 元素应用 class 或 id 属性，但是更常见的情况是只应用其中一种。这两者的主要差异是，class 用于元素组（类似的元素，或者可以理解为某一类元素），而 id 用于标识单独的唯一的元素。

HTML:

```php+HTML
<p class="tip"><span>提示：</span>... ... ...</p>
```

CSS:

```css
p.tip span {
	font-weight:bold;
	color:#ff9955;
	}
```

