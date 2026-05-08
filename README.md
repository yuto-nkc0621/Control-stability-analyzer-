# Control-stability-analyzer-
# A basic Python tool for control system stability analysis. / Pythonを用いて作成した、制御系の安定性を解析するツールです。

import control as ctrl
import matplotlib.pyplot as plt

#伝達関数の定義
print("Transfer Functions: G(s)= num / (a*s^2 + b*s + c)")

#伝達関数分子
print("Enter the numerator of the G(s)")
num = float(input("Here:"))

#伝達関数分母
print("Put the Denominator of the G(s)(a*s^2 + b*s + c)")
a = float(input("a: "))
b = float(input("b: "))
c = float(input("c: "))

num = [num]
den = [a, b, c]
G = ctrl.TransferFunction(num, den)

#伝達関数を表示
print("Your G(s):")
print(G)

#極を出します
poles = ctrl.poles(G)
zeros = ctrl.zeros(G)

print("poles:")
print(poles)
print("zeros:")
print(zeros)

#安定性を求めます
if all(p.real < 0 for p in poles):
    print("judge: stable")
elif any(p.real > 0 for p in poles):
    print("judge: unstable")
else:
    print("judge: Marginal Stability")
    

#ステップ応答を計算
t, y = ctrl.step_response(G)

#グラフ描画＆タイトル
plt.plot(t, y)
plt.title("Step Response")

#ⅹ軸ｙ軸
plt.xlabel("Time")
plt.ylabel("Output")

#グリッド表示
plt.grid(True)

#グラフ表示
plt.show()
