# midi-transcriber

MIDI in over USB -> `midi-transcriber` -> printed on receipt printer

```python
from escpos.printer import Usb
p = Usb(0x0456, 0x0808, 0, 0x81, 0x03)
# convert -resize x420 -rotate 90 test.png test2.png
p.image("../test2.png")
```

```ly
\version "2.22.0"

#(define default-toplevel-book-handler
  print-book-with-defaults-as-systems )

#(ly:set-option 'backend 'eps)

upper = \relative c'' {
  \clef treble
  \key c \major
  \time 4/4

  a4 b c d
}

lower = \relative c {
  \clef bass
  \key c \major
  \time 4/4

  a2 c
}

\score {
  \new PianoStaff \with { instrumentName = "Piano" }
  <<
    \new Staff = "upper" \upper
    \new Staff = "lower" \lower
  >>
  \layout { }
  \midi { }
}
```
