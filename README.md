#piller

piller turns a normal textarea into a flexible typeahead that can search different data sets and display the selection as a pill of text within the textarea. This was inspired by the implementation of Facebook's comment box at-referencing.

##Implementation
The way piller displays the pills is a bit of an illusion. A "decorator" element is perfectly overlaid on top of a textarea. This decorator has `pointer-events: none` set as a CSS style which allows mouse events to fall through to the textarea below. As the user types into the textarea, every key stroke is captured and recreated as HTML within the decorator such that every character is perfectly aligned between the decorator and the textarea. In order to prevent fuzzy or darker than expected font display, the decorator has the `color: transparent` style applied. When a pill is added, piller stores meta data containing the start index and end index where the pill should be positioned in respect to the plain text value. Using these indexes, piller creates an HTML element inside the decorator to display the pill style at the perfect position. Every pill element in the decorator has `pointer-events: all` to capture mouse events and focus, and `color: initial` to display the text within the pill.

##Install piller

```
npm install --save piller
```

##Usage
```
var piller = require('piller');

var pillerInstance = piller.create(containerElement, pillCorpus, options, optionalTextarea);
```

*containerElement*:
- HTML Element to build piller within.
- Note: this element needs to be exclusively devoted to piller (e.g. don't use document.body)

*pillCorpus*:
- Array of *pills* that can be searched, selected, and turned into a pill
- See below on how to create a pill

*options*: object to configure piller with the following properties
- *scrollable*: allows the container to scroll if value is truthy
- *excludeStoredPillsNotFoundInCorpus*: disregards pill found within a *pillerModelValue* (see below) that are not found in the pillCorpus
- *searchDebounceTime*: time in milliseconds to debounce searching behavior on every text input
- *storageKey*:
- *storageInterface*: defaults to *localStorage*. Supplies a custom object for caching model values by *storageKey*.
- *onModelChange*:
- *showSearchMatches*:
