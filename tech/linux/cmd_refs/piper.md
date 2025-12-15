# piper


```bash
echo 'Welcome to the world!' | ./piper --model en_GB-jenny_dioco-medium.onnx --output_file welcome.wav
```

```bash
echo 'The original machine had a base-plate of pre-fabulated amulite,
surmounted by a malleable logarithmic casing in such a way that the
two spurving bearings were in a direct line with the pentametric fan.
The latter consisted simply of six hydrocoptic marzelvances, so
fitted to the ambifacient lunar waneshaft that side fumbling was
effectively prevented.  The main winding was of the normal lotus-o-delta
type placed in panendermic semi-boloid slots in the stator, every
seventh conductor being connected by a non-reversible tremie pipe to
the differential girdlespring on the "up" end of the grammeters.' | ./piper --model en_GB-cori-high.onnx --output_file turbo_encabulator.wav
```

```bash
echo 'This sentence is spoken first. This sentence is synthesized while the first sentence is spoken.' | \
  ./piper --model en_US-lessac-medium.onnx --output-raw | \
  aplay -r 22050 -f S16_LE -t raw -
```

```bash
echo 'The original machine had a base-plate of pre-fabulated amulite,
surmounted by a malleable logarithmic casing in such a way that the
two spurving bearings were in a direct line with the pentametric fan.
The latter consisted simply of six hydrocoptic marzelvances, so
fitted to the ambifacient lunar waneshaft that side fumbling was
effectively prevented.  The main winding was of the normal lotus-o-delta
type placed in panendermic semi-boloid slots in the stator, every
seventh conductor being connected by a non-reversible tremie pipe to
the differential girdlespring on the "up" end of the grammeters.' | \
  ./piper --model en_GB-cori-high.onnx --output-raw | \
  aplay -r 22050 -f S16_LE -t raw -
```


