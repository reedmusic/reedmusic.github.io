# Installations

## 1: 4h33

```ruby
# John Cage composed 4'33" in 1952

# This piece is 4h33: an order of magnitude better.

# The chord is built of four fifths.
# C plays every minute
# G plays every 3 minutes
# D plays every 7 minutes
# A plays every 13 minutes

# [C, D, G, A] plays every 273 minutes.


use_bpm 1
use_synth :tri
use_synth_defaults  attack: 0.5, release: 1.25, cutoff: 100

with_fx :reverb, room: 1 do
  with_fx :hpf, cutoff: 50 do
    with_fx :flanger, mix: 0.4 do
      
      live_loop :a do
        play :c3, pan: -1
        sleep 1
      end
      
      live_loop :b do
        play :g3, pan: -0.5
        sleep 3
      end
      
      live_loop :c do
        play :d4, pan: 0.5
        sleep 7
      end
      
      live_loop :d do
        play :a4, pan: 1
        sleep 13
      end
    end
  end
end


live_loop :vinyl do
  sample :vinyl_hiss, amp: 0.9
  sleep sample_duration :vinyl_hiss
end
```

# 2: Probabalistic Drums

```ruby
live_loop :drums do
  use_bpm 60
  with_fx :reverb, mix: 0.4 do
    with_fx :echo, mix: 0.2, phase: 2 do
      
      sample :loop_amen, slice: 0, rate: 0.5 if one_in(8)
      sample :loop_amen, slice: 2, rate: 1 if one_in(8)
      sample :loop_amen, slice: 7, rate: -0.7 if one_in(20)
      sample :drum_cymbal_closed, amp: 0.5 if one_in(2)
      sample :drum_cymbal_closed if one_in(3)
      
      
      ## Bass
      use_synth :tb303
      play scale(:e1, :minor_pentatonic, num_octaves: 2).choose,
        release: 0.15,
        cutoff: rrand(60, 80),
        amp: rrand(0.8, 0.9) if one_in(3)
      
      ## Sound Effects
      sample :ambi_lunar_land, amp: 0.75, rate: -0.5 if one_in(100)
      sample :ambi_piano, amp: 1.5, pitch: rrand_i(-4, 5) if one_in(50)
      sample :ambi_glass_hum,
        rate: [1, 3.0/2, 2.0/3].choose,
        pan: rrand(-1,1) if one_in(60)
      sleep 1.0/8
    end
    
  end
end
```

### 3. Onset Remix

```ruby
live_loop :sample do
  use_random_seed 100
  
  c = [130,130,130,130,70,100].tick
  r = [0.4, 0.4, 0.4, 0.4, 0.7, 0.6].look
  
  use_sample_defaults cutoff: c
  
  
  with_fx :reverb, mix: r do
    with_fx :pan, mix: 0.8 do
      
      
      
      16.times do
        sample "Users/School/Desktop/blind2.wav", onset: [0,1,2,3,4,5,7,8,9,11,13,14,17,20].choose,
          rate: [1,1,-1].choose
        sleep 1.0/8
      end
      
      8.times do
        sample "Users/School/Desktop/blind2.wav", onset: [0,1,2,3,4,5,7,8,9,11,13,14,17,20].choose,
          rate: 3.0/2
        sleep 1.0/8
      end
      
      8.times do
        sample "Users/School/Desktop/blind2.wav", onset: [0,1,2,3,4,5,7,8,9,11,13,14,17,20].choose,
          rate: ((3.0/2)**2)/2
        sleep 1.0/8
      end
      
    end
  end
end


live_loop :bass do
  with_fx :gverb, mix: 0.1 do
    sample :bd_zome, amp: 1.5
    sleep 1
  end
end
```
