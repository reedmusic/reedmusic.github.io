1. For [**HINTS**](#hints) see below
2. For [**CHALLENGE WIKI**](https://github.com/MrReedSWCHS/Sonic-Pi/wiki) click here

---

# Hints

## Looping

Loops start with `loop do` and end with `end`

```ruby
loop do
  play 80
  sleep 1
end
```

---

## Don't get trapped! Use in_thread

Once your loop starts it will not stop until you press STOP. To make your loop run with the next thing down in your code you can use `in_thread`.

Here the loop and the sample will start at the same time.

```ruby
in_thread do
  loop do
    play 80
    sleep 1
  end
end

sample :bd_zome
```

If you have LOTS of things starting at the same time, you will need an `in_thread` on everything except the bottom thing:

```ruby
in_thread do
  loop do
    play 80
    sleep 1
  end
end

in_thread do
  sample :bd_zome
end

sample :ambi_drone
```

---

## Repeats

Instead of looping forever you can use `10.times` to say repeat something 10 times.

You still need a `do` and `end`:

```ruby
10.times do
  play 80
  sleep 1
end
```

---

## Change the speed

You need `use_bpm` and then a number to change the speed.

---

## Numbers or Notes?

You can play numbers or note names. `play 60` is the same as `play :c4`.

***

# Want more ideas?

If these are too simple for you, you need to look at the [**Challenge Wiki**](https://github.com/MrReedSWCHS/Sonic-Pi/wiki)
