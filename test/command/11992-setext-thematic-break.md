Lines of only dashes or equals must not be mistaken for thematic
breaks or setext heading underlines when read back (#11992).

```
% pandoc -f native -t gfm
[Para [Str "---"]]
^D
\---
```

```
% pandoc -f native -t gfm
[Para [Str "Lead", LineBreak, Str "==="]]
^D
Lead\
\===
```

```
% pandoc -f native -t gfm
[Para [Str "Lead", LineBreak, Str "---"]]
^D
Lead\
\---
```

Wrapping must not put an unescaped run of equals or dashes on its
own line:

```
% pandoc -f native -t gfm --columns=20
[Para [Str "aaaaaaaaaaaaaaaaaaa", Space, Str "==="]]
^D
aaaaaaaaaaaaaaaaaaa
\===
```

With `smart`, the writer already escapes runs of dashes, so nothing
more is needed (regression guard):

```
% pandoc -f native -t markdown
[Para [Str "---"]]
^D
\-\--
```

```
% pandoc -f native -t markdown
[Para [Str "lead", Space, Str "==="]]
^D
lead \===
```
