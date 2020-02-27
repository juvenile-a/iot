#coding: utf-8
import math

#設定
maxspeed = 0.002 #[sec/step]
accel = 30 #[rad/sec^2]加速度
decel = 30 #[rad/sec^2]減速度
position_deg = 180 #[deg]移動量

#共通
position_rad =  position_deg * math.pi / 180 #[deg]移動量
a_deg = 0.9 #[deg/step]ステップ角（度）
n = position_deg / a_deg #[step]総ステップ数
k = 360 / a_deg #[step]1回転当たりのステップ数
a_rad = 2 * math.pi / k #[rad/step]ステップ角（ラジアン）
m = accel / decel #減速に対しての加速の比率

#三角駆動
t_triangular = math.sqrt(2 * position_rad * (m + 1) / accel) #[sec]トータル時間
ta_triangular = t_triangular / (m + 1)#[sec]加速時間
v = accel * ta_triangular #速度
na_triangular = n / (m + 1) #[step]加速ステップ数
nd_triangular = n - na_triangular #[step]減速ステップ数

#台形駆動
vm = 1 / maxspeed * a_rad #[rad/sec]最高速度
ta_trapezoidal = vm / accel #[sec]加速時間
tad_trapezoidal = ta_trapezoidal * (m + 1) #[sec]加速+減速時間
sad_trapezoidal = accel * tad_trapezoidal ** 2 / (2 * (m + 1)) #[rad]加速+減速移動量
nad_trapezoidal = sad_trapezoidal / a_rad #[step]加速＋減速ステップ数
na_trapezoidal = nad_trapezoidal / (m + 1) #[step]加速ステップ数
nd_trapezoidal = nad_trapezoidal - na_trapezoidal #[step]減速ステップ数
#t_trapezoidal = #[sec]トータル時間

#三角駆動か台形駆動になるか判断
if v <= vm:
    accel_end = na_triangular #[step]加速終了ステップ
    decel_start = nd_triangular #[step]減速開始ステップ
    print('三角駆動')
else:
    accel_end = na_trapezoidal #[step]加速終了ステップ
    decel_start = nd_trapezoidal #[step]減速開始ステップ
    print('台形駆動')

counter = []
i = 0
c0 = 0.676 * math.sqrt(2 * a_rad / accel)
counter.append(c0)
print(i , counter[i])

while True:
    i += 1
    if i >= n: break
    elif i < accel_end:
        cn = counter[-1] - 2 * counter[-1] / (4 * i + 1)
        counter.append(cn)
        print(i , counter[i])
    elif i >= decel_start:
        cn = counter[-1] - 2 * counter[-1] / (4 * (i - n) + 1)
        counter.append(cn)
        print(i , counter[i])
    else:
        counter.append(maxspeed)
        print(i , maxspeed)
        
#print()
