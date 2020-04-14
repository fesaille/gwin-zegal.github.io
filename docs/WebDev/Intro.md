# Web Developpment


[WHATWG spec](https://html.spec.whatwg.org/multipage/)


First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.


## HTML semantic elements

> Elements, attributes, and attribute values in HTML are defined (by this specification) to have certain meanings (semantics). For example, the ol element represents an ordered list, and the lang attribute represents the language of the content.
> 
> These definitions allow HTML processors, such as Web browsers or search engines, to present and use documents and applications in a wide variety of contexts that the author might not have considered.
>

## Web components


<badge-doc href="https://developer.mozilla.org/en-US/docs/Web/Web_Components" message="MDN" color="lightgrey"></badge-doc>


JavaScript file defines a class called `PopUpInfo`, which extends `HTMLElement`. Inside the constructor, all the functionality the element will have when an instance of it is instantiated.

!!! Example 
	Create a badge similar to the one at the top of the page:

	```javascript linenums="1"
	class DocBadge extends HTMLElement {
	constructor() {
		// Always call super first in constructor
		super();

		// Create a documentation badge
		var shadow = this.attachShadow({mode: 'open'});

		var wrapper = document.createElement('span');
		wrapper.setAttribute('class','myBadge');

		var href = this.hasAttribute('href')?this.getAttribute('href'):'img/default.png';
		var alt = this.hasAttribute('alt')?this.getAttribute('alt'):'Documentation';
		var label = this.hasAttribute('label')?this.getAttribute('label'):'docs';
		var message = this.hasAttribute('message')?this.getAttribute('message'):'stable';
		var color = this.hasAttribute('color')?this.getAttribute('color'):'brightgreen';
		var logo = this.hasAttribute('logo')?this.getAttribute('logo'):'Read-the-docs';

		var src = `https://img.shields.io/badge/${label}-${message}-${color}?style=flat&logo=${logo}`;
		
		var link = document.createElement('a');
		link.setAttribute('target','_blank');
		link.setAttribute('href', href);

		var img = document.createElement('img');
		img.setAttribute('src', src);
		img.setAttribute('alt', alt);

		shadow.appendChild(wrapper);
		wrapper.appendChild(link);
		link.appendChild(img);
	}
	}

	// register it
	customElements.define('badge-doc', DocBadge);
	```

	Usage:
	```html
	<badge-doc href="https://developer.mozilla.org/en-US/docs/Web/Web_Components" message="MDN" color="lightgrey"></badge-doc>
	```



## Resources

- [Shield badges](https://shields.io/)
- [Simple icons](https://simpleicons.org/)
