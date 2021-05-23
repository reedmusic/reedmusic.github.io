# Sequencer

## 1. Generating rhythm

Use the `amp:` option for `play` or `sample` to change its volume, or amplitude.

`play :c4, amp: 0.75`

Use square brackets and `.tick` through them:

```ruby
live_loop :sequencer do
  
  use_bpm 120
  
  sample :drum_cymbal_closed, amp:
    [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0].tick
  
  sleep 1.0/4
  
end
```

## 2. Layers

Copy and paste, but don't forget to use `.look` instead of `.tick`

```ruby
live_loop :sequencer do
  
  use_bpm 120
  
  sample :drum_cymbal_closed, amp:
    [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0].tick
  
  sample :bd_haus, amp:
    [1,0,0,0, 1,0,0,0, 1,0,0,0, 1,1,0,0].look
  
  sample :drum_snare_hard, amp:
    [0,0,0,0, 1,0,0,0, 0,1,0,0, 1,0,0,1].look
  
  sleep 1.0/4
  
end
```

## 3. Ghost notes

Numbers between 0 and 1 for more subtle volume changes.

```ruby
live_loop :sequencer do
  
  use_bpm 120
  
  sample :drum_cymbal_closed, amp:
    [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0].tick
  
  sample :bd_haus, amp:
    [1,0,0,0, 1,0,0,0, 1,0,0,0, 1,1,0,0].look
  
  sample :drum_snare_hard, amp:
    [0,0.2,0,0, 1,0,0,0.1, 0,1,0,0, 1,0,0.75,0.25].look
  
  sleep 1.0/4
  
end
```

## Subtle layers

No need for each layer to be `.tick`ed.

Maybe some layers that just play every loop?

e.g. `sample :drum_cymbal_closed, amp: 0.2` for a subtle hi-hat hit.

```ruby
live_loop :sequencer do
  
  use_bpm 120
  
  sample :drum_cymbal_closed, amp:
    [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0].tick
  
  sample :drum_cymbal_closed, amp: 0.2
  
  sample :bd_haus, amp:
    [1,0,0,0, 1,0,0,0, 1,0,0,0, 1,1,0,0].look
  
  sample :drum_snare_hard, amp:
    [0,0.2,0,0, 1,0,0,0.1, 0,1,0,0, 1,0,0.75,0.25].look
  
  sleep 1.0/4
  
end
```


