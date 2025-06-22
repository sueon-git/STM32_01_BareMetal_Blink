STM32 첫걸음: 베어메탈(Bare-Metal) LED 깜빡이기
1. [프로젝트 소개]
NUCLEO-F401RE 보드를 사용, 가장 기본적인 펌웨어 작성 실행

운영체제(OS) 없이 C언어와 HAL 라이브러리만으로 하드웨어를 직접 제어하는 '베어메탈' 실행 목표

2. [개발 환경 및 사용 기술]
보드(MCU): NUCLEO-F401RE (STM32F401RET6)

개발 환경(IDE): STM32CubeIDE

핵심 기술:

C Language: 기본적인 C언어 문법 활용

Bare-Metal Programming: OS 없이 while(1) 무한 루프 기반으로 순차적 프로그램 제어

HAL (Hardware Abstraction Layer): ST사에서 제공하는 라이브러리

GPIO Control: 범용 입출력 핀을 출력으로 설정하여 LED 제어

3. [주요 구현 내용]
main 함수의 while(1) 루프 안에서 다음 두 가지 HAL 함수를 반복적으로 호출하여 LED를 깜빡이게 구현

// main.c의 while(1) 루프 내부
HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5); // LD2 LED의 상태를 계속해서 뒤집습니다.
HAL_Delay(1000);                      // 1초(1000ms) 동안 프로그램 실행을 멈춥니다.

HAL_GPIO_TogglePin(): 이 함수 하나로 GPIO 핀의 상태를 HIGH/LOW로 계속 전환하여 코드를 간결하게 유지

HAL_Delay(): 간단한 시간 지연을 만들어, 우리 눈에 LED가 1초 간격으로 깜빡이는 것처럼 보임. 이 함수가 호출되는 동안에는 MCU가 다른 일을 하지 않고 멈춤을 확인

4. [실행 결과]
NUCLEO-F401RE 보드의 녹색 사용자 LED(LD2)가 1초 간격으로 규칙적으로 깜빡이는 것을 확인

동작 영상 (GIF): 
![Image](https://github.com/user-attachments/assets/3b9830d6-99b9-40dc-8286-2f18a3a2ce1a) 

5. [체크포인트]
궁금증 자아 : Bare-Metal과 FreeRTOS 차이가 뭘까, 만약 LED를 깜빡이면서 동시에 다른 일도 해야 한다면? 등등의 자연스러운 의문생김.