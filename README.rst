Dopo https://translate.google.com/toolkit

rimuovere eventualmente ``#, python-format`` da quelle stringhe che danno errore con poedit

Poi, con regex pycharm per le modifiche ``** testo ** --> **testo**``

find: ``\s\*\*\s([^*\n]+)\s\*\*``

replace: `` **$1**``
