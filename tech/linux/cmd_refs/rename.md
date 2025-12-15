# rename

```bash
brett@pentatonic:/data/Music/Thievery Corporation/The Cosmic Game [2005]$ ls
'01 - Thievery Corporation - Marching the Hate Machines (Into the Sun) ft. The Flaming Lips [Official].mp3'
'02 - Warning Shots.mp3'
'03 - Revolution Solution.mp3'
'04 - The Cosmic Game - The Cosmic Game.mp3'
'05 - Satyam Shivam Sundaram - The Cosmic Game.mp3'
'06 - Amerimacka.mp3'
'07 - Ambicion Eterna (Eternal Ambition) - The Cosmic Game.mp3'
'08 - Pela Janela (Through the Window) - The Cosmic Game.mp3'
'09 - Sol Tapado (The Covered Sun) - The Cosmic Game.mp3'
"10 - The Heart's a Lonely Hunter - The Cosmic Game.mp3"
'11 - Holographic Universe - The Cosmic Game.mp3'
'12 - Doors of Perception - The Cosmic Game.mp3'
'13 - Thievery Corporation - Wires and Watchtowers [Official Audio].mp3'
'14 - Thievery Corporation - The Supreme Illusion [Official Audio].mp3'
'15 - Thievery Corporation - The Time We Lost Our Way [Official Music Video].mp3'
'16 - Thievery Corporation - A Gentle Dissolve [Official Audio].mp3'
 cover.jpg
brett@pentatonic:/data/Music/Thievery Corporation/The Cosmic Game [2005]$ 
brett@pentatonic:/data/Music/Thievery Corporation/The Cosmic Game [2005]$ rename 's/ Thievery Corporation -//g' *.mp3
brett@pentatonic:/data/Music/Thievery Corporation/The Cosmic Game [2005]$ ls
'01 - Marching the Hate Machines (Into the Sun) ft. The Flaming Lips [Official].mp3'
'02 - Warning Shots.mp3'
'03 - Revolution Solution.mp3'
'04 - The Cosmic Game - The Cosmic Game.mp3'
'05 - Satyam Shivam Sundaram - The Cosmic Game.mp3'
'06 - Amerimacka.mp3'
'07 - Ambicion Eterna (Eternal Ambition) - The Cosmic Game.mp3'
'08 - Pela Janela (Through the Window) - The Cosmic Game.mp3'
'09 - Sol Tapado (The Covered Sun) - The Cosmic Game.mp3'
"10 - The Heart's a Lonely Hunter - The Cosmic Game.mp3"
'11 - Holographic Universe - The Cosmic Game.mp3'
'12 - Doors of Perception - The Cosmic Game.mp3'
'13 - Wires and Watchtowers [Official Audio].mp3'
'14 - The Supreme Illusion [Official Audio].mp3'
'15 - The Time We Lost Our Way [Official Music Video].mp3'
'16 - A Gentle Dissolve [Official Audio].mp3'
 cover.jpg
brett@pentatonic:/data/Music/Thievery Corporation/The Cosmic Game [2005]$ rename 's/ \[.*\]//g' *.mp3
brett@pentatonic:/data/Music/Thievery Corporation/The Cosmic Game [2005]$ ls
'01 - Marching the Hate Machines (Into the Sun) ft. The Flaming Lips.mp3'  "10 - The Heart's a Lonely Hunter - The Cosmic Game.mp3"
'02 - Warning Shots.mp3'                                                   '11 - Holographic Universe - The Cosmic Game.mp3'
'03 - Revolution Solution.mp3'                                             '12 - Doors of Perception - The Cosmic Game.mp3'
'04 - The Cosmic Game - The Cosmic Game.mp3'                               '13 - Wires and Watchtowers.mp3'
'05 - Satyam Shivam Sundaram - The Cosmic Game.mp3'                        '14 - The Supreme Illusion.mp3'
'06 - Amerimacka.mp3'                                                      '15 - The Time We Lost Our Way.mp3'
'07 - Ambicion Eterna (Eternal Ambition) - The Cosmic Game.mp3'            '16 - A Gentle Dissolve.mp3'
'08 - Pela Janela (Through the Window) - The Cosmic Game.mp3'               cover.jpg
'09 - Sol Tapado (The Covered Sun) - The Cosmic Game.mp3'
brett@pentatonic:/data/Music/Thievery Corporation/The Cosmic Game [2005]$ 

```
