
## Phasing a la Steve Reich
Two (or several?) `live_loop`s, each at a different tempo (e.g. `use_tempo 120`)

## Define variables that you can later control

Make sure the definition is in the `live_loop` or it will not update when you hit run again.

```

live_loop :chord do
  
  x = chord(:e4, :minor)
  
  play x.tick, release: 0.2
  sleep 1.0/8
  
end
```
