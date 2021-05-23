# Sequencer

## 1. Generating rhythm

Use the `amp:` option to change amplitude (for either synths or samples)

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

### Polyrhythm

Not all layers have to be the same length:

```ruby
live_loop :sequencer do
  use_bpm 120
  
  # Drums
  
  sample :drum_cymbal_closed, amp:
    [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0].tick
  
  sample :bd_klub, amp:
    [1,0,0,0,0].look
  
  sample :drum_tom_hi_soft, amp:
    [1,0.8,0,0,0.75,0,1,0,0,0,0].look
  
  sample :drum_tom_mid_soft, amp:
    [1,0.8,0,0,0.75,0,1,0,0].reverse.look
  
  sample :drum_cowbell, amp:
    [1,0,0, 1,0,0, 1,0,0, 1,0,0, 1,0,0, 1,1,0,1].look * 0.5
  
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

## 4. Subtle layers

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

## 4. Changing volume and randomisation

Use some maths e.g. `* 0.5` after the `amp:` values to change all volumes:

```
sample :drum_cowbell, amp:
      [1,0,0,1, 0,0,1,0, 0,0,1,0, 0,1,0,0].look * 0.5
```

Use `if` and `one_in(x)` to set up random drum hits. Good for toms!

```ruby
  sample :drum_tom_lo_hard, pan: -0.5, amp: 0.5 if one_in(12)
  sample :drum_tom_hi_hard, pan: -0.5, amp: 0.5 if one_in(10)
  sample :drum_tom_mid_soft, pan: 0.5, amp: 0.5 if one_in(5)
```
  
## 5. FX on specific layers

Using `:echo` on the cowbell...

```ruby
live_loop :sequencer do
  use_bpm 120
   
  # Drums
  
  sample :drum_cymbal_closed, amp:
    [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0].tick
  
  sample :drum_cymbal_closed, amp: 0.2
  
  sample :bd_haus, amp:
    [1,0,0,0, 1,0,0,0, 1,0,0,0, 1,1,0,0].look
  
  sample :drum_snare_hard, amp:
    [0,0.2,0,0, 1,0,0,0.1, 0,1,0,0, 1,0,0.75,0.25].look
  
  # More cowbell
  
  with_fx :echo, mix: 0.2 do
    sample :drum_cowbell, amp:
      [1,0,0,1, 0,0,1,0, 0,0,1,0, 0,1,0,0].look * 0.5
  end
  
  # Toms
  
  sample :drum_tom_lo_hard, pan: -0.5, amp: 0.5 if one_in(12)
  sample :drum_tom_hi_hard, pan: -0.5, amp: 0.5 if one_in(10)
  sample :drum_tom_mid_soft, pan: 0.5, amp: 0.5 if one_in(5)
  
  
  sleep 1.0/4
end
```

## 6. Bassline

* `chord()` to define some notes
* `.choose` to randomise
* `release: 0.2` option to shorten notes
* `amp: [0,1,1,1,1,0.5].choose` to introduce some random rhythm. 


```ruby
use_synth :tb303
play chord(:b1, 'm6*9', num_octaves: 2).choose, release: 0.2, amp: [0,1,1,1,1,0.5].choose
```

### In context:

```ruby
live_loop :sequencer do
  use_bpm 120
  
  # Drums
  
  sample :drum_cymbal_closed, amp:
    [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0].tick
  
  sample :drum_cymbal_closed, amp: 0.2
  
  sample :bd_haus, amp:
    [1,0,0,0, 1,0,0,0, 1,0,0,0, 1,1,0,1].look
  
  sample :drum_snare_hard, amp:
    [0,0.2,0,0, 1,0,0,0.1, 0,1,0,0, 1,0,0.75,0.25].look
  
  # More cowbell
  
  with_fx :echo, mix: 0.2 do
    sample :drum_cowbell, amp:
      [1,0,0,1, 0,0,1,0, 0,0,1,0, 0,1,0,0].look * 0.5
  end
  
  # Toms
  
  sample :drum_tom_lo_hard, pan: -0.5, amp: 0.5 if one_in(12)
  sample :drum_tom_hi_hard, pan: -0.5, amp: 0.5 if one_in(10)
  sample :drum_tom_mid_soft, pan: 0.5, amp: 0.5 if one_in(5)
  
  # Bass
  
  use_synth :tb303
  play chord(:b1, 'm6*9', num_octaves: 2).choose, release: 0.2, amp: [0,1,1,1,1,0.5].choose
  
  
  sleep 1.0/4
end
```


## 7. Methods

'Methods' allow you to change those lists of values.

We have already used `.choose`. Here are some other uses:

* `.tick` will tick through each value
* `.look` will read the value at the current `.tick` position
* `.choose` will choose a random value
* `.reverse` will reverse the list
* => `.reverse.tick` and `.reverse.look` will tick/look through the reversed list
* `.take(x)` will take the first x values from the list
* => `.take(x).tick` will tick through the first x values
* => `.reverse.take(x).tick` will tick through the first x values in the reversed list

```ruby
live_loop :sequencer do
  use_bpm 120
  
  seq = [1,0,1,1, 0,1,0,0, 1,0,0,0, 1,1,0,0]
  
  
  # Drums
  
  sample :drum_cymbal_closed, amp: seq.tick
  
  sample :bd_fat, amp: seq.reverse.look
  
  sample :elec_filt_snare, amp: seq.take(5).look * 0.5,
    finish: 0.25, release: 0.5
  
  sample :elec_triangle, amp: seq.reverse.take(9).look * 0.5,
    finish: 0.25, release: 0.5
  
  sleep 1.0/4
  
end
```
