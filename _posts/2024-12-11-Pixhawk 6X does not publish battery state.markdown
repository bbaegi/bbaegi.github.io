---
layout: post
title:  "Pixhawk Jetson Baseboard does not publish battery state"
date:   2024-12-11 18:00:00 +0900
categories: jekyll update
published: true
---

Holybro Pixhawk6X Jetson Baseboard with Nvidia Jetson Orin NX 16GB 모델을 기반으로 X500 V2 프레임 기반의 쿼드콥터 제작 및 세팅 중 발견한 증상.

PM02D 파워모듈로부터 전송받아서 QGroundControl SW 에서 모니터링 되어야 할 배터리 상태정보가 보이지 않는 현상이 있다.

해결법은 파라미터 세팅에 있었다.
파워 모듈도 여러 세대를 거치면서 사용하는 칩셋에 따라 드라이버들이 달라진 것으로 판단되는데, PX4 1.14.3 버전에서 기본으로 설정되어있는 파라미터가 Pixhawk Jetson Baseboard 패키지에 포함되어있는 PM02D 파워모듈과 호환이 되지 않는다.

해당 부분에 영향을 주는 파라미터는
- SENS_EN_INA226
- SENS_EN_INA228
- SENS_EN_INA238
류의 파라미터를 확인하면 되고, 본 경우에는 SENS_EN_INA226에서 SENS_EN_INA228을 활성화하는것으로 변경하여 문제를 해결하였다.