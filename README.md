# Daily GuLuGuLu Water

- 单片机学习仓库，希望我能从LED开始，直到年底完成**Daily GuLuGuLu Water**项目
- 一个利用esp32+蓝牙+wifi+压力传感器的检测每日喝水次数与喝水量的智能杯垫项目。
- 我真的很需要这个杯垫！

## 技术路线

- 利用压力传感器记录杯子放到杯垫上时的数值，经过一次喝水后，杯子重新放回杯垫，此时记录差值即为喝水量。
- 可以统计喝水的次数和每天的总的喝水量。
- 目前打算利用蓝牙或wifi实现与PC端和手机端的通信。（实时查看饮水量）

## 教程参考
1. [罗大富Bigrich-2023年最新 ESP32 Arduino 教程](https://www.bilibili.com/video/BV1RM4y1a7J5/)
2. [小智学长](https://space.bilibili.com/383943678)

## 模拟平台
- [wokwi](https://wokwi.com/)

## 参考文献
1. [Effects of Drinking Hot Water, Cold Water, and Chicken Soup on Nasal Mucus Velocity and Nasal Airflow Resistance](https://doi.org/10.1016/S0012-3692(15)37387-6)
2. [The effects of a hot drink on nasal airflow and symptoms of common cold and flu](https://www.researchgate.net/profile/Ronald-Eccles/publication/23790050_The_effects_of_a_hot_drink_on_nasal_airflow_and_symptoms_of_common_cold_and_flu/links/0deec518fe3376cd31000000/The-effects-of-a-hot-drink-on-nasal-airflow-and-symptoms-of-common-cold-and-flu.pdf)

<div align=center>
  <img src='images/water.jpg'>
</div>