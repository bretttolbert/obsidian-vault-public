# GNU graphviz

https://bretttolbert.com/creating-tree-graphs-with-graphviz

In this episode we'll be creating tree graphs using the graphviz DOT language. 

First we need to install the graphviz package:
```
sudo apt install -y graphviz
```

Now we'll create a simple graph. Copy the following DOT language into a file named `life.gv`:
```
digraph D {
  Life -> {Bacteria, Archaea, Eukaryota}
  Eukaryota -> {Plants, Fungi, Animals}
  Plants -> {Gymnosperms, Angiosperms}
  Animals -> {Vertebrates, Invertebrates}
  Vertebrates -> {Fish, Amphibians, Reptiles, Birds, Mammals}
}
```

Now we can generate a postscript file (similar to a pdf) with the following command:
```
dot -Tps life.gv -o life.ps
```
We can also generate a PNG image file with this command:
```
dot -Tpng life.gv -o life.png
```

![life.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627223890233/54jVdFQfs.png)

Now for a more complex example, try this taxonomy of political ideologies:

```
digraph D {
  Ideology -> {Other, Left, Right}
  Other -> {AnarchoPrimitivism}
  Left -> {Anarchism, Socialism, Liberalism}
  Liberalism -> {SocialDemocracy}
  Right -> {Neoliberalism, Libertarianism, Conservatism, Monarchism, Fascism}
  Fascism -> NazBols
  Libertarianism -> AnarchoCapitalism
  edge [arrowhead=onormal, style=dashed, color=orange]
  Stalinism -> NazBols [constraint=false]
  Liberalism -> {Neoliberalism, Neoconservatism, Libertarianism} [constraint=false]
  Socialism -> Fascism [constraint=false]
  Anarchism -> {AnarchoPrimitivism, AnarchoCapitalism} [constraint=false]
  edge [arrowhead=normal, style=solid, color=black]
  Conservatism -> {Paleoconservatism, Neoconservatism, Nationalism}
  Nationalism -> Trumpism
  Socialism -> {LibertarianMunicipalism, Marxism, Georgism}
  LibertarianMunicipalism -> DemocraticConfederalism
  Anarchism -> {SocialAnarchism, IndividualistAnarchism}
  IndividualistAnarchism -> {Egoism}
  SocialAnarchism -> {AnarchoSyndicalism, Inssurrectionary, Green}
  SocialAnarchism -> Mutualism [constraint=false]
  IndividualistAnarchism -> Mutualism
  SocialAnarchism -> LibertarianMunicipalism [constraint=false]
  Socialism -> SocialAnarchism [constraint=false]
  Marxism -> {LeftCommunism, Leninism, DemocraticSocialism}
  LeftCommunism -> {CouncilCommunism, Bordigism, Situationism}
  Leninism -> {Trotskyism, Maoism, Stalinism, Titoism}
  Maoism -> {MaoZedongThought, MLM, ThirdWorldism}
  Trotskyism -> Posadism
  Stalinism -> Hoxhaism
  edge [arrowhead=onormal, style=dashed, color=orange]
  Fascism -> Nationalism [constraint=false]
}
```

![ideologies_scaled.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627224383801/NC_KmIoZu.png)

Things to note: 
* `[constraint=false]` tells graphviz to ignore this edge for the purposes of layout, and just draw the edge between the nodes whereever they happen to be without rearranging them.
* `edge [arrowhead=onormal, style=dashed, color=orange]` is used to draw the orange dashed lines with open arrowheads, indicating weak or alleged associations between political ideologies, or appropriation of ideas. Obviously this is all highly debatable and I have no interest in debating it here, but now you have the source and can modify it to your heart's content.

Meta: How to resize png image with imagemagick so it will be small enough to upload to hashnode:
```
$ sudo apt install -y imagemagick
$ identify ideologies.png 
ideologies.png PNG 3221x635 3221x635+0+0 8-bit sRGB 275337B 0.000u 0:00.000
$ python3 -c 'print(3221 / 2)'
1610.5
$ convert ideologies.png -resize 1610 ideologies_scaled.png
$ identify ideologies_scaled.png 
ideologies_scaled.png PNG 1610x317 1610x317+0+0 8-bit sRGB 173525B 0.000u 0:00.000
```
