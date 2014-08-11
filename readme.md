This gist replicates a bug in the way Stylus imports files. If you import two files with the same filename, but different path, Stylus will silently ignore the second import. The behaviour is the same for both `@require` and `@import`.


```bash
$ git clone https://github.com/joshhunt/stylus-import-bug.git
$ cd stylus-import-bug
$ stylus main.styl
  compiled main.css
$ cat main.css
```

**Expected:**
```stylus
body {
  color: #000;
  padding: 20px;
}
```

**Actual:**
```stylus
body {
  color: #fff
  padding: padding-base;
}
```

I would expect for `variables.styl` to override the value of `text-color` to green, and set `padding-base` to `20px`. However that does not happen. An error is not thrown when importing `variables.styl`, it is just silently ignored.

Renaming `variables.styl` to anything else (and updating `main.styl`) get's the expected output.
