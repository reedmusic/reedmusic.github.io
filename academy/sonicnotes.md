Notes from Academy session 20/5/21

# Chords

```
play chord(:e4,:M7)

sleep 1

play [:e4, :g4, :b4]
```

# Envelopes and loops

```
live_loop :chords do
  
  play chord(:e4,:M7), attack: 8, release: 8
  
  sleep 2
  
  play chord(:a4,:M7), attack: 8, release: 8
  
  sleep 2
  
end
```


