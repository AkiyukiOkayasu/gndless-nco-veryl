# gndless_nco

unsigned modular phaseを生成するNCO primitiveです。波形変換は所有せず、オシレーターやASRCの位相源に使います。

公開APIは`FractionalPhaseAccumulator`、`Phase`、`Phasor`、`EocDetector`です。依存はVeryl stdのみです。

`Phase`は32bitのunsigned phase、`step_t`は符号付き48bit phase stepです。accumulatorは2の補数moduloでwrapし、`enable`停止中は状態を保持します。`Phasor`は同期reset、`phase_rst`を持ち、latencyは0（`phase`出力はregister更新後）です。1周期完了（End Of Cycle）は`EocDetector`を併設して検出します。

```veryl
inst nco: nco::FractionalPhaseAccumulator #( WIDTH: 32 ) (...);
```

検証: `veryl fmt --check && veryl check && veryl test && veryl build && veryl doc`。
