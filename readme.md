# zmk-config

This is my personal [ZMK firmware](https://github.com/zmkfirmware/zmk/) configuration. 
It is ported from my QMK configuration, which in turn is heavily inspired by Manna Harbour's
[Miryoku layout](https://github.com/manna-harbour/miryoku).

## Key features

- simple macro-implementation of combos and keymap to fit different physical
  keyboards[^1]
- home-row mods on base layer, sticky mods on `Nav` and `Num` layers
- most symbols can be accessed from the base layer via combos
- sticky shift on right thumb, double-tap activates caps-word
- backspace morphs into delete when shifted
- unicode layer with Greek letters for mathematical typesetting (implemented via preprocessor macros[^2]) 

![](img/keymap.png)

## A few thoughts on the combo setup

The combo layout is guided by two goals: (1) put all combos in easy-to-access locations,
and (2) make them easy to remember. Specifically:

- the top vertical-combo row is almost equivalent to the symbols on standard number rows,
  making them easy to remember
- the bottom vertical-combo row is set up symmetrically to facilitate memorization
  (subscript `_` aligns with superscript `^`; minus `-` aligns with `+`; division `/`
  aligns with multiplication `*`; logical-or `|` aligns with logical-and `&`; backslash
  `\` aligns horizontally with forward slash `/`)
- `!` and `?` are on home-row position for prime access
- parenthesis, brackets and braces are on the right-hand side for easy access when
  typing numbers
- a numlock shortcut (on `W + P`) is on the left-hand side for one-handed number-mode
- shortcuts for cut (on `X + D`), copy, and paste are on the left-hand side for
  one-handed usage when working with the mouse

[^1]: I use a 36-key layout per default. Additional thumb keys can be configured with
    the `EXTRA_BOT_L` and `EXTRA_BOT_R` macros. Additional "middle-keys" can be
    configured with the `EXTRA_MID` macro (see `planck_rev6.keymap` for an example).

    In order to consitently configure combos and [positional
    hold-taps](https://zmk.dev/docs/behaviors/hold-tap#positional-hold-tap-and-hold-trigger-key-positions)
    across keyboards with different physical key specifications, I use a set of "virtual
    location" macros which map key-positions in the layout to physical locations on the
    shield. These macros follow a common naming convention, starting with `LT0` for the
    first key on the **L**eft **T**op-row and ranging to `RB4` for the last key on the
    **R**ight **B**ottom-row. They need to be defined in the shield-specific keymap-file
    *before* sourcing the common `base.keymap`.

[^2]: This is my attempt at a simple user-space solution until unicode is natively
    supported. Check out `unicode.dtsi` for details and read
    [my write up here](https://github.com/zmkfirmware/zmk/issues/232#issuecomment-1163833880)
    for a few more pointers and some caveats.