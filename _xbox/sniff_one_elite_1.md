---
title:  "Xbox One Elite (Gen 1) Sniff"
layout: single
classes: wide
redirect_from:
  - /sniffs/XboxOneSniff.html

categories: [xbox]
tags: [xbox, one, elite, controller, usb, sniff]
---

This is close documentation for a sniff of an Xbox One Elite (Gen 1) packet sniff, for those learning how to read packet sniffs.


The title of each section in the document is following this format:

```
<Important Value> - <Bit Location> - <Name of Button Pressed>
```

## Numbering Scheme

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:02:1d:10:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:10:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
```

---

## Proposed Code Implementation

```
typedef struct {
    uint8_t command;
    uint8_t reserved1;
    uint8_t counter;
    uint8_t size;
    uint16_t buttons;
    uint16_t trigL, trigR;
    int16_t left, right;
    uint16_t true_buttons;
    uint16_t true_trigL, true_trigR;
    int16_t true_left, true_right;
    uint8_t paddle;
} XBOXONE_ELITE_IN_REPORT;
```
{: .language-c}

---

### `0x0010` - `Bit 04` - `A`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:02:1d:10:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:10:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
20:00:03:1d:00:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
```

### `0x0020` - `Bit 05` - `B`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:04:1d:20:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:20:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
20:00:05:1d:00:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
```

### `0x0040` - `Bit 06` - `X`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:06:1d:40:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:40:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
20:00:07:1d:00:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
```

### `0x0080` - `Bit 07` - `Y`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:08:1d:80:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:80:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
20:00:09:1d:00:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00:00:00:00:00:00:66:02:97:f8:d5:02:d7:fb:00
```

### Preset Switch Toggle from 1 to 2

Notice how `[32]` changes from `00` to `10` from previous packet. This change does not send its own packet. It just changes outgoing packets.

### `0x1000` - `Bit 12` - `Left Bumper`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:0b:1d:00:10:00:00:00:00:52:02:8f:f8:c4:02:ee:fb:00:10:00:00:00:00:52:02:8f:f8:c4:02:ee:fb:10
20:00:0c:1d:00:00:00:00:00:00:52:02:8f:f8:c4:02:ee:fb:00:00:00:00:00:00:52:02:8f:f8:c4:02:ee:fb:10
```

### `0x2000` - `Bit 13` - `Right Bumper`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:0d:1d:00:20:00:00:00:00:52:02:8f:f8:c4:02:ee:fb:00:20:00:00:00:00:52:02:8f:f8:c4:02:ee:fb:10
20:00:0e:1d:00:00:00:00:00:00:52:02:8f:f8:c4:02:ee:fb:00:00:00:00:00:00:52:02:8f:f8:c4:02:ee:fb:10
```

### `0x4000` - `Bit 14` - `Left Stick Click`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:71:1d:00:40:00:00:00:00:c8:09:16:17:c4:02:ee:fb:00:40:00:00:00:00:c8:09:16:17:c4:02:ee:fb:10
20:00:7d:1d:00:00:00:00:00:00:5a:0c:65:1c:c4:02:ee:fb:00:00:00:00:00:00:5a:0c:65:1c:c4:02:ee:fb:10
```

### `0x8000` - `Bit 15` - `Right Stick Click`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:b1:1d:00:80:00:00:00:00:09:08:cd:fb:2c:08:ed:01:00:80:00:00:00:00:09:08:cd:fb:2c:08:ed:01:10
20:00:c1:1d:00:00:00:00:00:00:09:08:cd:fb:53:0a:2b:01:00:00:00:00:00:00:09:08:cd:fb:53:0a:2b:01:10
```

### `0x0100` - `Bit 08` - `D-Pad Up`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:d6:1d:00:01:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:01:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
20:00:d7:1d:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
```

### `0x0200` - `Bit 09` - `D-Pad Down`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:d8:1d:00:02:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:02:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
20:00:d9:1d:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
```

### `0x0400` - `Bit 10` - `D-Pad Left`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:da:1d:00:04:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:04:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
20:00:db:1d:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
```

### `0x0800` - `Bit 11` - `D-Pad Right`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:dc:1d:00:08:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:08:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
20:00:dd:1d:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
```

### `0x0008` - `Bit 03` - `View`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:de:1d:08:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:08:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
20:00:df:1d:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
```

### `0x0004` - `Bit 02` - `Menu`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:e0:1d:04:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:04:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
20:00:e1:1d:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:00:00:00:00:00:00:09:08:cd:fb:b3:07:05:fb:10
```

### `0x0010` - `Bit 04` - `A`

Initiated using the Upper Left Paddle

Notice how `[4]` and `[18]` differ. Also notice the change in `[32]`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:cb:1d:10:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:11
20:00:cc:1d:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:10
```

### `0x0020` - `Bit 05` - `B`

Initiated using the Upper Right Paddle

Notice how `[4]` and `[18]` differ. Also notice the change in `[32]`
```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:cd:1d:20:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:12
20:00:ce:1d:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:10
```

### `0x0040` - `Bit 06` - `X`

Initiated using the Lower Left Paddle

Notice how `[4]` and `[18]` differ. Also notice the change in `[32]`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:cf:1d:40:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:14
20:00:d0:1d:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:10
```

### `0x0080` - `Bit 07` - `Y`

Initiated using the Lower Right Paddle

Notice how `[4]` and `[18]` differ. Also notice the change in `[32]`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:d1:1d:80:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:18
20:00:d2:1d:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:00:00:00:00:00:00:4c:04:5c:f8:17:03:b2:fb:10
```

### Preset Switch Toggle from 2 to 1

Notice how `[32]` changes from `10` to `00` from previous packet. This change does not send its own packet. It just changes outgoing packets.

### `0x1000` - `Bit 12` - `Left Bumper`

Remapping Upper Left Paddle to Left Bumper. Notice the change in `[32]`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:d4:1d:00:10:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:01
20:00:d5:1d:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00
```

### `0x2000` - `Bit 13` - `Right Bumper`

Remapping Upper Right Paddle to Right Bumper. Notice the change in `[32]`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:d6:1d:00:20:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:02
20:00:d7:1d:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00
```

### `0x0040` - `Bit 06` - `X`

Remapping Lower Left Paddle to X. Notice the change in `[32]`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:d8:1d:40:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:04
20:00:d9:1d:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00
```

### `0x0080` - `Bit 07` - `Y`

Remapping Lower Right Paddle to Y. Notice the change in `[32]`

```
00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
--------------------------------------------------------------------------------------------------
20:00:da:1d:80:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:08
20:00:db:1d:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00:00:00:00:00:00:74:04:5c:f8:2a:03:ee:fb:00
```