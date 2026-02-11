# advanced-system-software


Issues while committing
```bash
git switch main
```

# commit your current changes first (important)
```bash
git add -A
git commit -m "Save work"
```

```bash
# merge remote main into your main even if histories are unrelated
git fetch advanced-system-software
git merge --allow-unrelated-histories advanced-system-software/main
```

```bash
# then push
git push -u advanced-system-software main
```
