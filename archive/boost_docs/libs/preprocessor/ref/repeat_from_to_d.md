# BOOST_PP_REPEAT_FROM_TO_D

`BOOST_PP_REPEAT_FROM_TO_D` マクロは高速な横断的繰り返しを構築する。
これは最も効率的に `BOOST_PP_WHILE` に再入する。

## Usage

```cpp
BOOST_PP_REPEAT_FROM_TO_D(d, first, last, macro, data)
```

## Arguments

- `d` :
	利用可能な次の `BOOST_PP_WHILE` の繰り返し。

- `first` :
	繰り返しの下限。
	有効な値の範囲は `0` から `BOOST_PP_LIMIT_MAG` までである。

- `last` :
	繰り返しの上限。
	有効な値の範囲は `0` から `BOOST_PP_LIMIT_MAG` までである。

- `macro` :
	`macro(z, n, data)` という形の 3つ組の演算。
	このマクロは `BOOST_PP_REPEAT` によって、利用可能な次の繰り返しの深さ、現在の繰り返し回数、付属の `data` に展開される。

- `data` :
	`macro` に渡される付属のデータ。

## Remarks

このマクロは次のシーケンスに展開される:

```cpp
macro(z, first, data) macro(z, first + 1, data) ... macro(z, last - 1, data)
```

繰り返しの回数 (つまり、 `last - first` は `BOOST_PP_LIMIT_REPEAT` を越えてはならない。

`macro` に渡される `z` の値は利用可能な次の繰り返し次元を表す。
`_Z` 接尾辞をもつ他のマクロとその仲間は内部で、`BOOST_PP_REPEAT` を利用している -
例えば、 `BOOST_PP_ENUM_PARAMS` と `BOOST_PP_ENUM_PARAMS_Z` などである。
これらの `_Z` バージョンを使うことは厳密には必要ではないが、(`macro` に渡される) `z` の値をこれらのマクロに渡すことで、最も効率的に `BOOST_PP_REPEAT` に再入することが出来る。

この `z` の値を、単純に別のマクロに渡すのではなく、直接使うためには、`BOOST_PP_REPEAT_FROM_TO_D_z` を見よ。

## See Also

- [`BOOST_PP_LIMIT_MAG`](limit_mag.md)
- [`BOOST_PP_LIMIT_REPEAT`](limit_repeat.md)
- [`BOOST_PP_REPEAT_FROM_TO`](repeat_from_to.md)
- [`BOOST_PP_REPEAT_FROM_TO_D_z`](repeat_from_to_d_z.md)

## Requirements

Header: &lt;boost/preprocessor/repetition/repeat_from_to.hpp&gt;

