+++
title = 'SimulatedAnnealing'
date = 2024-08-13T21:00:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "heuristic"
]
+++
## 用途

$ f: D \rightarrow \mathbb{R} $の返り値が定義域$ D $で最大になるような$x \in D$を求める. 焼きなまし法です.

## 計算量

$ O\left(\text{epoch} \left \lceil \dfrac{\log \text{(target temp)} - \log {\text{(init  temp)}}}{\log \text{(cooling coef)}} \right \rceil \right ) $

## 使い方

### 宣言

```cpp
struct State{ // 状態を表す構造体
  double x;

  // f(x) = -x^4 + x^3 + x^2 + x
  // max f(x): 2.33.... (x = 1.28...)
  double eval(){ // 評価関数
    return -pow(x,4)+pow(x,3)+pow(x,2)+x;
  }
  void modify(){ // 遷移
    x += ((double)rand() / (RAND_MAX))-0.5;
  }
};

ESAnnealing<State> sa;
// sa内のStateの初期設定をする
sa.state.x=0;
```

`State`の中身を目的に応じて書き換えてください

### Hyperparameterの設定 & 焼なます

```cpp
// (epoch当たりの試行回数, 初期温度, 目標温度, 冷却係数)
sa.annealing(100,100000,0.1,0.99);
```

### 結果の参照

```cpp
// 結果はクラス内のstateで参照できる
std::cout << "Solution: " << "f(x) = " << sa.state.eval() << ", x = " << sa.state.x << std::endl;
```

## 実装

```cpp
template <class T>
class ESAnnealing
{
public:
  T state;

  void annealing(double epoch, double temperature, double temperature_target, double coolingcoef, unsigned int seed = 42, bool verbose = true)
  {
    assert(0 <= coolingcoef and coolingcoef < 1);
    assert(temperature >= temperature_target);
    srand(seed);
    double initscore = state.eval();
    double beststate_score = initscore;
    T beststate = state;
    int estimeted_epoch = std::ceil((std::log(temperature_target) - std::log(temperature)) / std::log(coolingcoef));
    if (verbose)
      std::cout << std::fixed << std::setprecision(6)
                << "ESAnnealing started with:" << "\n"
                << "| epoch       " << epoch << "\n"
                << "| temperature " << temperature << "\n"
                << "| target temp " << temperature_target << "\n"
                << "| coolingcoef " << coolingcoef << "\n"
                << "| seed        " << seed << "\n"
                << "| est epoch   " << estimeted_epoch << "\n"
                << std::flush;
    int cnt = 0;
    while (temperature > temperature_target)
    {
      for (int i = 0; i < epoch; i++)
      {
        T newstate = state;
        newstate.modify();
        double statescore = state.eval();
        double newstatescore = newstate.eval();
        double delta = newstatescore - statescore;

        if (0 < delta)
        {
          state = newstate;
        }
        else if (frand() > std::exp(delta / temperature))
        {
          state = newstate;
        }

        if (beststate_score < newstatescore)
        {
          beststate_score = newstatescore;
          beststate = newstate;
        }
      }
      temperature *= coolingcoef;

      if (verbose)
        std::cout << cnt << "/" << estimeted_epoch - 1 << " temp: " << temperature << " eval: " << beststate_score << std::endl;

      cnt++;
    }
    state = beststate;
    if (verbose)
      std::cout << "annealed: " << initscore << "->" << beststate_score << std::endl;
  }

private:
  double frand()
  {
    return ((double)rand() / (RAND_MAX));
  }
};
```

from [github.com/romophic/ESAnnealing](https://github.com/romophic/ESAnnealing)

## Verify

//TODO
