# Sequencer

## Generating rhythm

Use the `amp:` option for `play` or `sample` to change its volume, or amplitude.

`play :c4, amp: 0.75`

Use square brackets and `.tick` through them:

```
live_loop :sequencer do
  
  use_bpm 120
  
  sample :drum_cymbal_closed, amp:
    [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0].tick
  
  sleep 1.0/4
  
end
```
