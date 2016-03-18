% yo
% hoo
% orz

# theme.. 哭哭


# 今天第一個題目

## {data-background="arr.jpg"}

<h2>使用 sdl2, sdl2-cairo, cairo 和 JuicyPixels</h2>
<h3>來讀/繪圖的崩潰歷程</h3>
測試一下文字尺寸

##

先來整理一下各套件是怎麼儲存圖片的..

* This
* Is
    * _Nothing_
    * __But__
        * ___A___
        * ~~Normal~~
        * Sentence

## JuicyPixels {.headline}

### A

...

### B

...

## JuicyPixels {.headline_alt}

### A *A*

...

### B

...

## JuicyPixels  {data-background="#DDF"}

```{.haskell}
import qualified Data.Vector.Storable as V

data Image a = Image
  { imageWidth  :: {-# UNPACK #-} !Int
  , imageHeight :: {-# UNPACK #-} !Int
  , imageData   :: V.Vector (PixelBaseComponent a)}
```

e.g. `V.Vector PixelRGBA8`{.haskell} or `V.Vector PixelCMYK16`

##

Canvas 可以...

```{.haskell}
data Canvas a = ...
```
```{.haskell}
Instances
    Functor Canvas
    Applicative Canvas
    Monad Canvas
    MonadIO Canvas
```
```{.haskell}
... = do
  background $ gray 102
  fill $ red 255 !@ 128
  noStroke
  rect $ D 200 200 100 100
  ...
```

##

但是

>  wrapper around the Cairo `Render`{.haskell} monad, providing a Processing-style API.

<p class="fragment">
那我何必呢? 直接用 Cairo 的 `Render`{.haskell} 就好啦~ orz
</p>

##

乾脆兩種都做：

```{.haskell}
class Pixel px => RenderablePixel px where
    drawPx :: (V2 Int, px) -> Canvas ()

class Pixel px => RenderablePixelC px where
    renderPx :: (V2 Int, px) -> Render ()
```

連結： [sdl2-cairo-image](https://hackage.haskell.org/package/sdl2-cairo-image),  [Render.hs](https://github.com/jaiyalas/sdl2-cairo-image/blob/master/src/SDL/Cairo/Image/Render.hs)

## Then..

* lots of bug..
* Vector-to-Vector
* rendering with `Renderer`
