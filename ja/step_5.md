## Pythonプログラミングインタフェースを使用する

Minecraftを起動し世界を創り上げたら、 `Tab`キー アプリケーションメニューからPython 3を開き、ウィンドウを左右に移動させます。
コマンドを直接Pythonウィンドウに入力するか、ファイルを作成してコードを保存してもう一度実行することができます。
ファイルを作成する場合は、`File > New window` 、`File > Save`. の順に選択します。ホームフォルダまたは新しいプロジェクトフォルダに保存することをお勧めします。

まず、Minecraftライブラリをインポートし、ゲームへの接続を作成し、"Hello world" というメッセージをポストしてテストします。
```python
from mcpi.minecraft import Minecraft

mc = Minecraft.create()

mc.postToChat("Hello world")
```


コマンドを直接Pythonウィンドウに入力する場合は、各行の後に `Enter` を押してください。ファイルの場合は`Ctrl + S`で保存し、 `F5`. で実行します。コードが実行されると、ゲームの画面にメッセージが表示されます。

### あなたの場所を見つける

現在地を見つけるには、次のように入力します

```python
pos = mc.player.getPos()
```

`pos` にはあなたの場所が含まれています。 `pos.x`, `pos.y` and `pos.z`で座標セットの各部分にアクセスします。

別の方法として、座標を別々の変数にするには、Pythonのアンパック手法を使用するのが良い方法です。

```python
x, y, z = mc.player.getPos()
```

 `x`, `y`, `z` には、それぞれの位置座標が含まれています。 `x`  `z`は歩行方向（前後左右）、`y`は上下方向です。

 `getPos()` はその時点のプレーヤーの位置を返します。位置を移動する場合は、関数を再度呼び出すか、格納された位置を使用する必要があります。

### テレポート

あなたの現在の場所を見つけるだけでなく、テレポートする特定の場所を指定することもできます。

```python
x, y, z = mc.player.getPos()
mc.player.setPos(x, y+100, z)
```
これはプレイヤーを空中の100の座標に運びます。これは、空の真ん中にテレポートして、あなたが始めた場所にまっすぐに戻ることを意味します。

別の場所にテレポートしてみてください！

### ブロックを設定する

 `mc.setBlock()`を使用して、与えられた座標セットに1つのブロックを配置することができます。

```python
x, y, z = mc.player.getPos()
mc.setBlock(x+1, y, z, 1)
```

あなたが立っているところに石ブロックが現れます。それがあなたのすぐ前になければ、それはあなたの横にあるかもしれません。 Minecraftウインドウに戻り、あなたの目の前に灰色のブロックが現れるまで、マウスを使ってその場で回転してください。
![](images/mcpi-setblock.png)

 `set block`に渡される引数は`x`, `y`, `z` `id`. `(x, y, z)`は世界の位置を指しています。（プレイヤーが  `x + 1`で立っている場所から1ブロック離れて指定されています `id` 配置したいブロックのタイプを表します。`1`は石です。

あなたが試すことができる他のブロック

```
Air:   0
Grass: 2
Dirt:  3
```

ブロックが見えたら、別のものに変更してみてください

```python
mc.setBlock(x+1, y, z, 2)
```


目の前で灰色の石ブロックに変化が見られるはずです！

![](images/mcpi-setblock2.png)

#### ブロック定数

名前を知っていれば、ブロックを設定するためにinbuiltブロック定数を使うことができます。しかし、最初に別の`import`が必要になります。

```python
from mcpi import block
```

今度はブロックを配置するために次のように書くことができます

```python
mc.setBlock(x+3, y, z, block.STONE.id)
```

ブロックIDは簡単に推測することができます。すべてのCAPSを使用するだけですが、ここではその名前に慣れさせるためのいくつかの例を示します。

```
WOOD_PLANKS
WATER_STATIONARY
GOLD_ORE
GOLD_BLOCK
DIAMOND_BLOCK
NETHER_REACTOR_CORE
```

### ブロックを設定する

ブロックのIDを知っていれば、それを変数として設定すると便利です。名前または整数IDを使用できます。

```python
dirt = 3
mc.setBlock(x, y, z, dirt)
```

または

```python
dirt = block.DIRT.id
mc.setBlock(x, y, z, dirt)
```

### 特殊ブロック


余分なプロパティを持ついくつかのブロックがあります。たとえば、色を指定できる特殊な設定を持つWoolです。これを設定するには、`setBlock`のオプションの第4パラメータを使用します。

```python
wool = 35
mc.setBlock(x, y, z, wool, 1)
```

ここでは、4番目のパラメータ `1`はウールの色をオレンジ色に設定します。番目のパラメータがなければ、デフォルト (`0`) which is white. Some more colours are:

```
2: Magenta
3: Light Blue
4: Yellow
```

Try some more numbers and watch the block change!

Other blocks which have extra properties are wood (`17`): oak, spruce, birch, etc; tall grass (`31`): shrub, grass, fern; torch (`50`): pointing east, west, north, south; and more. See the [API reference](http://www.stuffaboutcode.com/p/minecraft-api-reference.html) for full details.

### Set multiple blocks

As well as setting a single block with `setBlock` you can fill in a volume of space in one go with `setBlocks`:

```python
stone = 1
x, y, z = mc.player.getPos()
mc.setBlocks(x+1, y+1, z+1, x+11, y+11, z+11, stone)
```

This will fill in a 10 x 10 x 10 cube of solid stone.

![](images/mcpi-setblocks.png)

You can create bigger volumes with the `setBlocks` function but it may take longer to generate!

