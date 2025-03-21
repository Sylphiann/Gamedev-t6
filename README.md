# Tutorial 6 Game Development
Menu and In-Game Graphical User Interface

Nama : Favian Naufal  
NPM  : 2006597802

## Penjelasan fitur Tambahan

 1. **Tombol pada layar game over untuk kembali ke menu utama**  

Pada fitur ini, tombol **Main Menu** ditambahkan pada layar game over sekaligus dengan tombol **Try Again**. Implementasi fitur tersebut dilakukan dengan Menggunakan `VBoxContainer` di dalam sebuah `MarginContainer` seperti yang ditunjukkan pada struktur *scene* berikut ini:

```
[ROOT] ColorRect (GameOver)
└─ MarginContainer
    └─ VBoxContainer
        ├─ Label (Game Over)
        ├─ LinkButton (TryAgainButton)
        └─ LinkButton (MainMenuButton)
```

Sehingga dengan struktur berikut, Layar *Game Over* akan tertata secara vertikal.  

Kedua *node* `LinkButton` yang dibuat juga diberikan *attachment script* `New_Button.gd` dan juga *signal* yang sama dengan `LinkButton` yang telah diimplementasikan pada *Exercise* yang dilakukan dalam membuat *button* `New Game` pada *Main Menu*, dengan mengisi *exported variable* `scene_to_load` dengan `Level 1` untuk *button* "Try Again?" dan `mainmenu` untuk *button* "Main menu" 

2. **Fitur Select Stage**
 
Implementasi fitur layar *Select Stage* juga tidak jauh berbeda dari implementasi *Main menu* yang telah dilakukan pada *exercise* sebelumnya. Dengan membuat scene baru `StageSelect.tscn` dengan struktur yang sama dengan *scene* `GameOver.tscn` seperti berikut ini:

```
[ROOT] ColorRect (StageSelect)
└─ MarginContainer
    └─ VBoxContainer
        ├─ Label (Stage Select)
        ├─ LinkButton (Level1Button)
        └─ LinkButton (Level2Button)
```
Dengan implementasi yang sama terhadap *scene* layar *Game Over* memberikan *attachment script* `New_Button.gd` dan *signal* yang sama terhadap seluruh `LinkButton` yang ada, dan mengubah *value* `scene_to_load` untuk masing-masing level.

3. ***Life Counter*** untuk *scene Level 2*

*Life Counter* yang telah diimplementasikan pada *exercise* sebelumnya belum diberikan pada *gameplay* pada `Level 2`. Maka dari itu, cukup dilakukan *copy-paste* kedua node yang sama terhadap `Level 2`.

```
[ROOT] Node2D (Level 2)
├─ ...
└─ CanvasLayer
    └─ MarginCounter (LifeCounter)
```

Hal lain yang juga tidak kalah penting adalah implementasi *Life Counter Reset* ketika pemain mendapatkan layar `Game Over` dengan menambahkan `Global.lives = 3` pada *script* `New_Button.gd` sehingga menjadi berikut ini:

```
extends LinkButton

@export var scene_to_load: String

func _on_pressed() -> void:
	print(scene_to_load)
	Global.lives = 3
	get_tree().change_scene_to_file(str("res://scenes/" + scene_to_load + ".tscn"))

```