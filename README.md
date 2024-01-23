# MustGo_STM32
NUCLEO-F429ZI 보드를 사용하였음.
서보모터 동작을 위해 tim2의 ch3, ch4를 pwm으로 구성하였으며,
라즈베리파이와 통신하기 위해 uart2 를 세팅하였음(nvic 인터럽트 추가)

# prerequisite
INSTALL stm32cubeIde

# pwm
1. tim2의 경우 apb1 버스를 사용하므로 해당 클럭에 따라 pwm 주기 계산.
2. 본인의 서보모터는 20ms 주기 사용
3. prescaler 84-1, ARR reg 20000-1 로 설정하여 주기 50hz(20ms)로 pwm 파형 주파수 변환
4. servo motor 의 데이터시트 : 
 ① pwm period 20ms, 50hz
 ② duty cycle 1~2ms
 => 제어를 위한 펄스 폭(듀티사이클) : 1ms~2ms(5%~10%)
5. n% = pulse/(value of arr register) = x/20000
 ① if pulse = 1000, n% = 5%
 ② if pulse = 2000, n% = 10%