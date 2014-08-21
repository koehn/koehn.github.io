---
layout: techpost
title: Handy bash stuff I never knew
---

Somehow after using `bash` as my shell of choice for the past fifteen years or so, I've learned something new.

It turns out you can open the current command line into an editor, make your changes there, and then execute the modified command. This is incredibly useful for those long, tricky commands, or when you need to make complex edits.

Sadly the default editor is `emacs`. This is a shame, because

1.  `emacs` isn't installed by default on all Unices
2.  `vi` is a vastly superior editor (because I know it and not `emacs`; see above)You can change the editor bash uses to VI by simply setting the `EDITOR` variable at shell startup (e.g., `.bashrc`, `/etc/bash.bashrc`).

    export EDITOR=vi # or vim if you prefer
