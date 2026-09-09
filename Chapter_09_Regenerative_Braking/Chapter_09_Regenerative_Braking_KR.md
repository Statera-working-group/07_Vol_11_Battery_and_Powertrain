**Volume 11. Battery and Powertrain**

# Chapter 09. Regenerative Braking

## 09.01. Regenerative Braking Topology

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

회생 제동(Regenerative Braking)은 이동 중인 로봇이나 전기 차량(Electric Vehicle)이 감속할 때 보유한 운동 에너지(Kinetic Energy)를 다시 전기 에너지(Electrical Energy)로 변환한다. 구동 모터(Traction Motor)는 토크를 발생시키는 액추에이터(Actuator)로만 동작하는 대신, 회전 방향과 반대되는 토크가 명령되면 발전기(Generator)로 전환된다. 생성된 전력은 모터 드라이브(Motor Drive)를 통해 직류 전력 시스템(DC Power System)으로 전달되며, 기계식 마찰 브레이크(Mechanical Friction Brake)에서 열로 소모해야 하는 에너지를 감소시킨다.

회생 제동의 기본 토폴로지(Topology)는 3상 인버터(Three-Phase Inverter)와 BLDC 또는 영구자석 동기 모터(PMSM, Permanent Magnet Synchronous Motor)의 양방향 동작(Bidirectional Operation)과 밀접하게 관련된다. 구동 시에는 배터리(Battery)의 전기 에너지가 직류 링크(DC Link)와 인버터(Inverter)를 거쳐 모터로 전달된다. 회생 제동 시에는 실제 전력(Real Power)의 흐름이 반대로 바뀌어 모터 축(Motor Shaft)의 기계 에너지가 3상 전기 에너지로 변환되고, 인버터를 통해 처리된 후 직류 링크를 거쳐 배터리 방향으로 반환된다.

일반적인 3상 브리지(Three-Phase Bridge)는 프리휠링 경로(Freewheeling Path)를 포함하는 6개의 제어형 반도체 스위치(Controlled Semiconductor Switch)로 구성된다. 물리적인 회로 구성은 모터 구동과 제동 사이에서 그대로 유지될 수 있지만, 스위칭 전략(Switching Strategy)이 전자기 토크(Electromagnetic Torque)와 전력 흐름의 방향을 결정한다. 따라서 인버터, 게이트 드라이버(Gate Driver), 직류 링크 부품(DC-Link Component), 제어 시스템(Control System)이 양방향 에너지 전달을 지원한다면 별도의 구동 변환기(Traction Converter)가 필요하지 않은 경우가 많다.

회생 제동은 로터(Rotor)가 계속 회전하고 있는 상태에서 제어기가 음의 토크(Negative Torque)를 요청할 때 시작된다. 자속 기준 제어(FOC, Field-Oriented Control)는 회전 방향과 반대되는 전자기 토크를 발생시키도록 토크 생성 전류 성분(Torque-Producing Current Component)의 극성을 설정할 수 있다. 이에 따라 모터는 구동계(Drivetrain)로부터 기계 에너지를 회수한다. 이러한 동작 상태에서는 로터 위치(Rotor Position), 상전류(Phase Current), 직류 링크 전압(DC-Link Voltage), 요구 감속도(Requested Deceleration), 배터리 허용 충전 전력(Allowable Battery Charging Power)을 지속적으로 평가해야 한다.

직류 링크(DC Link)는 인버터와 에너지 저장 시스템(Energy Storage System) 사이의 핵심 전기적 인터페이스(Electrical Interface)를 형성한다. 모터에서 생성된 에너지는 먼저 직류 링크 전압을 상승시키거나 유지하며, 이후 해당 에너지를 받아들일 수 있는 부하(Load)로 전달되어야 한다. 배터리 기반 로봇에서는 일반적으로 배터리가 주요 에너지 저장 대상이 된다. 직류 링크 커패시터(DC-Link Capacitor)는 생성 전력의 빠른 과도 변화와 배터리 및 상위 제어 시스템(Supervisory Control System)의 상대적으로 느린 응답 사이의 순간적인 차이를 흡수한다.

배터리 직접 연결 구조(Direct Battery-Connected Architecture)는 회생 전류(Regenerative Current)가 별도의 고전력 변환 단계 없이 인버터 직류 버스(DC Bus)에서 배터리 방향으로 흐를 수 있기 때문에 매력적이다. 이 구조는 부품 수, 전도 손실(Conduction Loss), 비용 및 패키징 부피(Packaging Volume)를 줄일 수 있다. 그러나 실제 회생 제동은 생성된 직류 버스의 전기적 조건이 배터리 전압, 배터리 관리 시스템(BMS, Battery Management System)의 제한, 컨택터(Contactor) 상태, 배선 용량 및 셀(Cell)의 허용 충전 전류와 호환될 때만 가능하다.

구동 직류 링크(Traction DC Link)와 배터리 사이에 양방향 DC-DC 컨버터(Bidirectional DC-DC Converter)를 포함하는 토폴로지는 회생 에너지 전달을 더욱 정밀하게 제어할 수 있다. 컨버터는 순간적인 인버터 측 전압과 독립적으로 배터리 충전 전류를 조절할 수 있으며, 모터 버스(Motor Bus)와 배터리가 서로 다른 전압 범위에서 동작하는 파워트레인(Powertrain)을 지원할 수 있다. 이러한 유연성은 충전 상태(SOC, State of Charge)에 따라 배터리 전압이 크게 변화하거나 여러 직류 버스가 함께 사용되는 시스템에서 특히 유용하다.

중간 단계에 양방향 컨버터(Bidirectional Converter)를 추가하면 반도체 손실(Semiconductor Loss), 자기 부품(Magnetic Component), 제어 복잡성(Control Complexity), 열 부하(Thermal Load), 질량 및 비용이 증가한다. 따라서 해당 컨버터는 자동적으로 적용하기보다 시스템 수준(System Level)에서 필요성을 판단해야 한다. 비교적 좁은 배터리 전압 범위를 사용하는 소형 자율이동로봇(AMR, Autonomous Mobile Robot)은 직접 회생 방식을 선택할 수 있지만, 보다 복잡한 파워트레인은 직류 링크와 배터리 측 전압을 분리하여 제어하는 구조의 이점을 얻을 수 있다.

회생 제동 능력은 인버터만으로 결정할 수 없는데, 배터리가 일시적으로 생성된 전력을 받아들이지 못할 수 있기 때문이다. 높은 충전 상태(SOC), 지나치게 낮거나 높은 셀 온도(Cell Temperature), 과도한 셀 전압(Cell Voltage), 충전 전류 제한(Charging-Current Restriction), 통신 오류(Communication Fault), 배터리 컨택터 개방(Open Battery Contactor) 등은 회생 제동을 제한하거나 완전히 금지할 수 있다. 따라서 배터리 관리 시스템(BMS)은 동작 한계(Operating Limit)를 제공하며, 모터 제어기(Motor Controller)는 이를 허용 가능한 음의 토크 또는 회생 전력 한계(Regenerative-Power Boundary)로 변환해야 한다.

배터리가 생성된 에너지를 모두 흡수하지 못하는 경우 토폴로지는 직류 링크 전압을 제어할 다른 방법을 제공해야 한다. 제동 초퍼(Braking Chopper)는 전압이 정의된 임계값(Threshold)을 초과하면 직류 버스에 제동 저항(Braking Resistor)을 연결할 수 있다. 초과된 전기 에너지는 배터리로 반환되는 대신 열로 변환된다. 이러한 동적 제동(Dynamic Braking)은 에너지 회수를 포기하지만 제어 가능한 감속을 유지하고 위험한 직류 버스 과전압(DC-Bus Overvoltage)을 방지하는 중요한 수단을 제공한다.

실제 파워트레인은 회생 제동(Regenerative Braking), 저항 기반 동적 제동(Resistor-Based Dynamic Braking), 기계식 제동(Mechanical Braking)을 결합할 수 있다. 배터리와 전기 시스템이 에너지를 받아들일 수 있는 동안에는 회생 제동을 우선적으로 사용한다. 제동 저항은 허용 충전 능력을 초과하는 전기 에너지를 처리할 수 있으며, 마찰식 또는 전기기계식 브레이크(Electromechanical Brake)는 나머지 제동 토크와 정지 상태 유지 기능을 담당한다. 이러한 제동 경로는 서로 배타적인 기술이 아니라 상호 보완적인 계층으로 구성된다.

저속 동작(Low-Speed Operation)은 회생 제동 토폴로지의 또 다른 중요한 한계이다. 회전 속도가 감소하면 일반적으로 생성 가능한 전압과 회수 가능한 전력이 감소하므로 영속도(Zero Speed)에 가까워질수록 회생 제동의 효과가 떨어진다. 따라서 차량이나 로봇은 최종 정지 및 정지 상태 유지를 위해 다른 제동 메커니즘(Braking Mechanism)으로 전환해야 한다. 이러한 특성은 빈번한 정밀 정지(Precise Stop), 도킹 동작(Docking Maneuver), 경사면 운행을 수행하는 자율이동로봇(AMR)에서 특히 중요하다.

회생 제동 토폴로지는 빠른 과도 현상(Transient Event)도 처리할 수 있어야 한다. 자율이동로봇(AMR)은 수 밀리초(Millisecond) 이내에 가속 상태에서 제동 상태로 전환될 수 있으며, 이에 따라 인버터의 전력 방향과 직류 링크 전류(DC-Link Current)가 빠르게 반전될 수 있다. 따라서 직류 링크 정전용량(DC-Link Capacitance), 전류 감지(Current Sensing), 전압 감지(Voltage Sensing), 게이트 제어(Gate Control), 컨택터 동작 및 보호 임계값(Protection Threshold)을 상호 조정해야 한다. 제어 지연이 지나치게 크면 회생 전류가 감소하거나 대체 에너지 소산 경로가 활성화되기 전에 버스 전압이 상승할 수 있다.

회생 제동 과정의 에너지 흐름(Energy Flow)은 개념적으로 휠(Wheel)의 운동이 구동계를 통해 모터에 토크를 전달하고, 이후 인버터에서 전기적 변환을 거쳐 직류 링크에서 안정화된 다음 배터리 방향으로 전달되는 과정으로 설명할 수 있다. 정상적인 구동 상태와 반대되는 이러한 관계는 전기 파워트레인(Electric Powertrain) 설계의 기본 원리이다. 이러한 양방향 구조(Bidirectional Structure)를 통해 동일한 모터와 인버터 하드웨어가 차량 가속뿐만 아니라 운동 에너지의 제어된 회수에도 사용될 수 있다.

회생 전류 경로(Regenerative Current Path)는 도체(Conductor), 커넥터(Connector), 퓨즈(Fuse), 컨택터(Contactor), 전력 분배 장치(PDU, Power Distribution Unit)의 설계에도 영향을 미친다. 최대 구동 전류만을 기준으로 선정한 부품은 역방향 전류 능력(Reverse-Current Capability), 과도 열 발생(Transient Heating), 차단 특성(Interruption Behavior), 측정 방향 등을 충분히 고려하지 못할 수 있다. 전류 센서(Current Sensor)는 양방향 전력 흐름을 구분해야 하며, 보호 로직(Protection Logic)은 정상적인 회생 전류를 비정상적인 역전류로 오인하지 않아야 한다.

고장 처리(Fault Handling)는 회생 제동이 차량의 운동 제어(Motion Control)를 배터리 및 고전력 직류 네트워크(High-Power DC Network)와 직접 연결하기 때문에 특히 중요하다. BMS 통신 손실, 인버터 고장, 직류 링크 과전압, 전류 센서 고장, 절연 고장(Isolation Fault), 예상하지 못한 컨택터 개방은 정상적인 에너지 회수 경로를 갑자기 제거할 수 있다. 제동 아키텍처(Braking Architecture)는 이러한 상태를 신속하게 감지하고 회생 토크를 안전하게 감소시키며 필요한 감속 기능을 동적 제동 또는 기계식 제동으로 전환해야 한다.

모바일 로봇(Mobile Robot)에서 회생 제동 토폴로지는 궁극적으로 단순한 인버터 기능이 아니라 시스템 수준의 에너지 및 제동 아키텍처(System-Level Energy and Braking Architecture)로 다루어져야 한다. 모터, 인버터, 직류 링크, 배터리, BMS, 선택적인 양방향 컨버터, 제동 저항, 기계식 브레이크, 센서 및 상위 제어기(Supervisory Controller)가 변화하는 속도와 배터리 조건에 따라 협력해야 한다. 올바르게 통합된 구조는 예측 가능한 정지 성능(Stopping Performance), 전기적 보호(Electrical Protection), 파워트레인 신뢰성(Powertrain Reliability)을 유지하면서 효율적인 에너지 회수를 가능하게 한다.

## 09.02. Energy Recovery Rate

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

에너지 회수율(Energy Recovery Rate)은 회생 제동 시스템(Regenerative Braking System)이 감속 과정에서 이용 가능한 운동 에너지(Kinetic Energy)와 위치 에너지(Potential Energy)를 저장하고 재사용할 수 있는 전기 에너지(Electrical Energy)로 얼마나 효과적으로 변환하는지를 나타낸다. 이는 모터 효율(Motor Efficiency)만으로 결정되지 않는다. 전체 에너지 경로에는 구동계(Drivetrain), 구동 모터(Traction Motor), 인버터(Inverter), 직류 링크(DC Link), 선택적 DC-DC 컨버터(Optional DC-DC Converter), 배터리(Battery), 제어 시스템(Control System)이 포함되며 각 변환 단계에서 손실이 발생한다.

이론적으로 회수할 수 있는 에너지(Theoretical Recoverable Energy)는 움직이는 플랫폼(Moving Platform)의 기계 에너지(Mechanical Energy)에서 시작한다. 병진 운동(Translational Motion)의 경우 운동 에너지는 차량 질량과 속도의 제곱에 비례하며 E = 1/2 mv²로 표현된다. 회전하는 휠, 기어, 축, 모터 로터(Motor Rotor)에도 회전 운동 에너지(Rotational Kinetic Energy)가 저장된다. 경사로를 내려갈 때에는 중력 위치 에너지(Gravitational Potential Energy)도 추가적으로 회생 변환에 이용될 수 있다.

운동 에너지(Kinetic Energy)는 속도의 제곱에 따라 증가하므로 차량 속도(Vehicle Speed)는 회수 가능한 에너지의 양에 큰 영향을 미친다. 질량이 일정한 상태에서 속도가 두 배가 되면 병진 운동 에너지는 약 네 배가 된다. 따라서 고속에서의 감속은 저속 정지보다 훨씬 많은 에너지를 회수할 기회를 제공하지만, 인버터와 배터리는 이에 따라 증가하는 회생 전력(Regenerative Power)을 처리할 수 있어야 한다.

에너지 회수율(Energy Recovery Rate)은 제동 과정에서 이론적으로 이용 가능한 기계 에너지와 실제로 에너지 저장 시스템(Energy Storage System)으로 반환된 전기 에너지의 비율로 표현할 수 있다. 예를 들어 100 kJ의 기계 에너지를 이용할 수 있고 그중 65 kJ가 배터리에 도달했다면 유효 회수율(Effective Recovery Ratio)은 65%이다. 이러한 시스템 수준(System-Level)의 값에는 변환 손실과 운전 또는 안전상의 제한으로 회수하지 못한 에너지가 모두 포함된다.

모터-발전기 효율(Motor-Generator Efficiency)은 에너지 회수율에 영향을 미치는 첫 번째 주요 요소 중 하나이다. 회생 제동 시 구동 모터는 축 동력(Shaft Power)을 전기 전력으로 변환하면서 동손(Copper Loss), 철손(Magnetic Loss), 기계적 마찰 손실(Mechanical Friction Loss), 기타 속도 의존적 손실(Speed-Dependent Loss)을 발생시킨다. 따라서 효율 맵(Efficiency Map)은 모터 속도와 토크에 따라 변화하며, 효율이 높은 영역에서 회생 제동을 수행하면 매우 낮은 속도나 불리한 토크 조건보다 훨씬 많은 에너지를 회수할 수 있다.

인버터(Inverter)는 또 하나의 에너지 변환 단계를 형성한다. 반도체 전도 손실(Semiconductor Conduction Loss), 스위칭 손실(Switching Loss), 데드타임 영향(Dead-Time Effect), 게이트 구동 소비 전력(Gate-Drive Consumption), 직류 링크 손실(DC-Link Loss)은 모터에서 직류 버스(DC Bus)로 전달되는 전기 에너지를 감소시킨다. 따라서 높은 인버터 효율은 효과적인 회생 제동에 중요하지만, 단일 최대 효율 수치가 아니라 실제 회생 운전 속도 및 토크 범위 전체에서 효율을 평가해야 한다.

직류 링크(DC Link)와 배터리 사이에 양방향 DC-DC 컨버터(Bidirectional DC-DC Converter)가 설치되어 있다면 해당 컨버터의 효율도 회수 에너지에 영향을 미친다. 컨버터는 더 넓은 전압 범위에서 배터리 충전을 제어함으로써 전체 에너지 활용도를 높일 수 있지만 추가적인 스위칭 및 전도 손실을 발생시킨다. 따라서 설계 시에는 추가 변환 손실과 전압 불일치(Voltage Mismatch) 또는 충전 제한 때문에 회수하지 못했을 에너지를 포착할 수 있는 능력 사이의 절충(Tradeoff)을 고려해야 한다.

배터리 충전 수용 능력(Battery Charge Acceptance)은 실제 시스템에서 가장 중요한 제한 요소가 되는 경우가 많다. 배터리 관리 시스템(BMS, Battery Management System)은 충전 상태(SOC, State of Charge), 셀 전압(Cell Voltage), 온도(Temperature), 건강 상태(SOH, State of Health), 팩 운전 조건(Pack Operating Condition)에 따라 회생 전류(Regenerative Current)를 제한할 수 있다. 거의 완전히 충전된 배터리는 상당한 기계 에너지가 존재하더라도 회생 에너지를 거의 받아들이지 못할 수 있으며, 저온 셀(Cold Cell) 역시 열화나 불안전한 운전 조건을 방지하기 위해 충전 전류를 크게 제한해야 할 수 있다.

회생 전력(Regenerative Power)과 회생 에너지(Regenerative Energy)는 명확하게 구분해야 한다. 전력(Power)은 순간적인 에너지 변환 속도를 의미하고, 에너지(Energy)는 전체 제동 과정에서 누적하여 회수된 양을 의미한다. 짧고 강한 제동은 높은 회생 전력을 발생시킬 수 있지만 총 회수 에너지는 상대적으로 제한적일 수 있다. 반대로 긴 내리막 주행은 중간 수준의 전력을 발생시키더라도 발전이 장시간 지속되기 때문에 훨씬 많은 에너지를 회수할 수 있다.

감속 요구량(Deceleration Demand)도 에너지 회수율에 영향을 미친다. 요구되는 제동 토크가 모터, 인버터, 배터리의 회생 능력(Regenerative Capability) 범위 안에 있다면 제동의 상당 부분을 전기적으로 수행할 수 있다. 그러나 비상 제동(Emergency Braking)이나 높은 감속도가 요구되는 상황에서는 필요한 토크가 회생 제동 한계를 초과할 수 있다. 이때 기계식 제동(Mechanical Braking)이 부족한 제동력을 제공해야 하며, 마찰열(Frictional Heat)로 변환된 운동 에너지는 회수할 수 없다.

낮은 차량 속도에서는 모터가 생성할 수 있는 전압과 이용 가능한 전력이 작아지기 때문에 일반적으로 회생 제동의 효과가 감소한다. 따라서 회생 제동만으로 영속도(Zero Speed)까지 모든 운동 에너지를 회수할 수는 없다. 최종적으로 기계식 또는 전기기계식 브레이크(Electromechanical Brake)가 정지 과정을 완료하고 차량을 정지 상태로 유지한다. 빈번한 저속 이동을 수행하는 자율이동로봇(AMR, Autonomous Mobile Robot)에서는 이러한 제한으로 인해 이론적인 계산값보다 실제 에너지 회수율이 크게 낮아질 수 있다.

제동 빈도(Braking Frequency)는 모바일 로보틱스(Mobile Robotics)에서 누적 에너지 회수 효과에 큰 영향을 미친다. 창고나 공장에서 운행되는 자율이동로봇(AMR)은 가속하고 짧은 거리를 이동한 뒤 감속하고 정지한 후 다시 가속하는 동작을 반복할 수 있다. 각각의 제동 과정에서 회수되는 에너지는 적을 수 있지만, 수천 번의 반복 운전 주기(Operating Cycle)가 누적되면 순 배터리 에너지 소비(Net Battery Consumption)를 의미 있게 감소시키고 충전 사이의 운전 시간을 증가시킬 수 있다.

차량 질량(Vehicle Mass)과 탑재 하중(Payload)도 회수 가능한 에너지의 크기에 영향을 미친다. 무거운 하중을 탑재한 자율이동로봇(AMR)은 동일한 속도로 이동하는 무부하 플랫폼보다 더 많은 운동 에너지를 보유한다. 이는 감속 시 회생 가능한 에너지를 증가시키지만 동시에 요구되는 제동 토크와 전력도 증가시킨다. 따라서 회생 제동 시스템은 총중량(Gross Mass), 최대 속도(Maximum Speed), 경사도(Gradient), 듀티 사이클(Duty Cycle), 허용 정지 거리(Allowable Stopping Distance)의 실제 조합을 기준으로 용량을 선정해야 한다.

도로 또는 바닥의 경사도(Gradient)는 또 다른 중요한 에너지원이다. 내리막 주행에서는 중력 위치 에너지(Gravitational Potential Energy)가 지속적으로 구동계로 전달된다. 회생 제동은 이 에너지의 일부를 배터리 충전 에너지로 변환하면서 동시에 차량 속도를 제어할 수 있다. 그러나 긴 내리막에서는 이용 가능한 운동 에너지보다 연속 회생 전력(Continuous Regenerative Power), 배터리 충전 수용 능력, 인버터 온도 또는 모터의 열적 능력(Thermal Capability)이 주요 제한 요소가 될 수 있다.

열적 조건(Thermal Conditions)은 반복적인 제동 과정에서 에너지 회수 성능을 점진적으로 감소시킬 수 있다. 모터 권선 온도(Motor Winding Temperature), 인버터 접합부 온도(Inverter Junction Temperature), DC-DC 컨버터 온도, 배터리 온도, 제동 저항 온도(Braking-Resistor Temperature)는 모두 디레이팅 한계(Derating Limit)를 발생시킬 수 있다. 따라서 단일 실험실 제동 시험에서 높은 회수율을 달성한 시스템이라도 지속적인 현장 운전에서는 다른 성능을 나타낼 수 있으며, 에너지 회수 평가는 반복 운전 주기와 열적 정상 상태(Thermal Steady-State)를 포함해야 한다.

제어 전략(Control Strategy)은 실제 에너지 회수 성능이 하드웨어 한계에 얼마나 근접할 수 있는지를 결정한다. 상위 제어기(Supervisory Controller)는 운전자 또는 자율주행 시스템의 제동 요구, 모터 능력, 직류 버스 전압(DC-Bus Voltage), 배터리 충전 제한, 시스템 온도를 기반으로 허용 가능한 회생 토크(Allowable Regenerative Torque)를 계산할 수 있다. 이러한 한계 안에서는 회생 제동을 우선 적용하고, 동적 제동(Dynamic Braking) 또는 기계식 제동이 나머지 토크를 제공하여 요구된 감속을 안전하고 예측 가능하게 만족시킨다.

에너지 회수율을 측정하려면 일관된 에너지 경계(Energy Boundary)를 정의해야 한다. 휠에서의 기계 에너지, 인버터 직류 단자(Inverter DC Terminal)에서의 전기 에너지, 실제로 배터리에 저장된 에너지는 서로 다른 측정 지점이므로 각각 다른 효율 값을 나타낸다. 전류(Current), 전압(Voltage), 속도(Speed), 토크(Torque), 시간(Time)을 충분한 정확도로 측정하여 순간 전력(Instantaneous Power)을 전체 제동 과정에 걸쳐 적분해야 하며, 중간 변환 효율과 전체 에너지 회수율을 혼동해서는 안 된다.

실제 자율이동로봇(AMR)의 평가에서는 제동 과정만 분석하기보다 회수된 에너지를 전체 임무 에너지(Total Mission Energy)와 비교해야 한다. 추진(Propulsion), 조향(Steering), 컴퓨팅(Computing), 센서(Sensor), 통신 장비(Communication Equipment), 냉각(Cooling), 보조 전장품(Auxiliary Electronics)은 운전 중 계속해서 전력을 소비한다. 높은 회생 변환 효율(Regenerative Conversion Efficiency)이 반드시 동일한 수준의 임무 시간 증가를 의미하지는 않는데, 전체 임무 에너지 가운데 회수 가능한 기계적 운동과 관련된 부분만 다시 배터리로 반환할 수 있기 때문이다.

따라서 에너지 회수율(Energy Recovery Rate)은 차량 동역학(Vehicle Dynamics), 모터-발전기 효율, 전력 전자(Power Electronics), 배터리 충전 수용 능력, 열적 한계(Thermal Limit), 제동 제어(Braking Control)를 연결하는 시스템 수준의 성능 특성(System-Level Performance Characteristic)이다. 이를 극대화하려면 단순히 회생 토크를 증가시키는 것만으로는 충분하지 않다. 시스템은 직류 버스 안정성(DC-Bus Stability), 배터리 보호(Battery Protection), 정지 요구 조건(Stopping Requirement), 부품 정격(Component Rating), 대체 제동 메커니즘(Alternative Braking Mechanism)으로의 예측 가능한 전환을 유지하면서 이용 가능한 기계 에너지를 효율적으로 회수해야 한다.

## 09.03. Battery Protection During Regen

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

회생 제동(Regenerative Braking) 중 배터리 보호(Battery Protection)는 구동 시스템(Traction System)이 일시적으로 배터리를 에너지원(Energy Source)에서 에너지 흡수원(Energy Sink)으로 전환하기 때문에 필수적이다. 모터에서 회수된 기계 에너지(Mechanical Energy)는 전기 전력(Electrical Power)으로 변환되어 인버터(Inverter)와 직류 링크(DC Link)를 통해 배터리로 반환된다. 이러한 역방향 전력 흐름(Reverse Power Flow)은 모든 제동 과정에서 배터리 팩(Battery Pack)의 허용 전압, 전류, 온도 및 셀 수준 운전 한계(Cell-Level Operating Limit) 내에서 유지되어야 한다.

배터리 관리 시스템(BMS, Battery Management System)은 회생 충전(Regenerative Charging)의 허용 여부를 결정하는 핵심 상위 관리 요소(Supervisory Element)이다. BMS는 팩 전압(Pack Voltage), 개별 셀 전압(Individual Cell Voltage), 전류(Current), 온도(Temperature), 충전 상태(SOC, State of Charge), 고장 상태(Fault Status)를 지속적으로 평가한다. 이러한 측정값은 모터 제어기(Motor Controller)에 전달할 수 있는 충전 한계(Charging Limit)로 변환되며, 이를 통해 회생 토크(Regenerative Torque)가 배터리의 충전 수용 능력을 무제한으로 가정하지 않도록 한다.

셀 과전압(Cell Overvoltage)은 회생 제동 중 가장 중요한 위험 요소 중 하나이다. 평균적인 팩 전압이 허용 범위에 있더라도 충전 상태가 더 높거나 가용 용량(Available Capacity)이 더 낮은 셀은 인접한 셀보다 먼저 상한 전압에 도달할 수 있다. 따라서 BMS는 전체 팩 전압에만 의존하지 않고 개별 셀 전압을 감시해야 한다. 가장 취약하거나 가장 많이 충전된 셀이 허용 가능한 회생 전류(Regenerative Current)를 결정할 수 있기 때문이다.

높은 충전 상태(SOC)는 배터리가 안전하게 받아들일 수 있는 회생 에너지의 양을 크게 감소시킨다. 배터리가 완전 충전에 가까워지면 셀 전압이 상한에 도달하기 전까지 남아 있는 에너지 여유(Energy Margin)가 매우 작아진다. 제어 시스템(Control System)은 강제적인 과전압 차단(Hard Overvoltage Trip)을 기다리는 대신 SOC가 증가함에 따라 허용 회생 전력(Allowable Regenerative Power)을 점진적으로 감소시켜야 한다. 이를 통해 에너지 회수에서 대체 제동 방식(Alternative Braking Method)으로 제어된 전환이 가능하다.

배터리 온도(Battery Temperature) 역시 안전한 회생 충전 능력을 결정한다. 리튬 기반 셀(Lithium-Based Cell)은 동작 온도 범위에 따라 충전 수용 특성이 달라지며, 매우 낮은 온도에서 충전하면 바람직하지 않은 전기화학적 현상(Electrochemical Effect)과 열화(Degradation)가 가속될 수 있다. 높은 온도에서는 추가적인 충전 손실이 열적 스트레스(Thermal Stress)를 증가시킬 수 있다. 따라서 BMS는 선택한 셀 화학계(Cell Chemistry)의 검증된 특성에 따라 온도 의존형 회생 전류 제한(Temperature-Dependent Regenerative Current Limit)을 적용한다.

리튬인산철 배터리(LFP, Lithium Iron Phosphate)와 니켈망간코발트 배터리(NMC, Nickel Manganese Cobalt)는 각각의 전기화학적 특성에 적합한 보호 전략(Protection Strategy)이 필요하다. LFP는 높은 열적 안정성(Thermal Stability)과 사이클 내구성(Cycle Durability)이 장점이지만 비교적 평탄한 전압-SOC 특성 때문에 정확한 SOC 판단이 어려울 수 있다. NMC는 높은 에너지 및 출력 밀도를 제공하지만 전압과 열적 조건을 세심하게 관리해야 한다. 두 경우 모두 회생 충전 한계는 검증된 셀 및 팩 운전 데이터(Validated Cell and Pack Operating Data)를 기반으로 설정해야 한다.

이동 중인 로봇이 강한 감속을 수행하면 회생 전류(Regenerative Current)가 빠르게 증가할 수 있다. 모터 제어기는 수 밀리초(Millisecond) 이내에 상당한 음의 토크(Negative Torque)를 명령할 수 있으며, 이에 따른 전기 전력은 즉시 직류 링크에 나타난다. 따라서 배터리 보호를 위해서는 전류 감지(Current Sensing), 직류 링크 전압 감시(DC-Link Voltage Monitoring), 인버터 제어(Inverter Control), BMS 제한 사이의 빠른 협조가 필요하다. 느린 통신만을 손상을 유발할 수 있는 과도 상태(Transient Condition)에 대한 유일한 보호 수단으로 사용해서는 안 된다.

허용 충전 전류(Allowable Charging Current)는 일반적으로 하나의 고정된 값이 아니라 동적 한계(Dynamic Limit)로 표현되어야 한다. 이 값은 SOC, 셀 온도, 팩 온도(Pack Temperature), 셀 전압 편차(Cell Voltage Spread), 건강 상태(SOH, State of Health), 최근 운전 이력(Operating History)에 따라 변화할 수 있다. 모터 제어기는 BMS가 제공하는 충전 전류 또는 충전 전력 제한을 배터리 상태에 따라 지속적으로 변화하는 최대 회생 토크(Maximum Regenerative Torque)로 변환할 수 있다.

직류 링크 과전압(DC-Link Overvoltage)은 생성된 회생 에너지가 충분히 빠르게 흡수되지 않고 있음을 나타내는 또 다른 중요한 지표이다. 기계적 발전 전력(Mechanical Generation Power)이 배터리와 기타 부하가 수용하는 전력을 초과하면 에너지가 직류 링크 커패시터(DC-Link Capacitor)에 축적되어 버스 전압(Bus Voltage)이 상승한다. 인버터 제어기는 이 전압을 신속하게 감시하고 반도체, 커패시터, 컨버터, 커넥터 또는 절연 시스템(Insulation System)의 정격을 초과하기 전에 회생 토크를 감소시켜야 한다.

제동 초퍼(Braking Chopper)와 제동 저항(Braking Resistor)은 배터리가 생성된 회생 에너지를 모두 받아들이지 못할 때 2차 보호 경로(Secondary Protection Path)를 제공할 수 있다. 직류 버스 전압(DC-Bus Voltage)이 정의된 임계값에 접근하면 초퍼가 저항을 연결하여 초과 전기 에너지를 열로 소산한다. 이를 통해 과도한 충전 전류를 배터리에 강제로 공급하지 않으면서 제동 토크를 유지할 수 있지만, 제동 저항의 온도와 연속 에너지 소산 능력(Continuous Energy-Dissipation Capability) 역시 보호되어야 한다.

기계식 제동(Mechanical Braking)은 배터리 보호가 에너지 회수 극대화보다 우선되어야 하기 때문에 반드시 필요하다. 높은 SOC, 온도, 전압, 전류, 통신 고장 또는 기타 배터리 조건으로 회생 전력이 제한되면 제동 제어기(Braking Controller)는 전기적 회생 제동을 감소시키고 그에 따라 기계식 제동을 증가시켜야 한다. 사용 가능한 회생 제동의 기여도가 갑자기 변하더라도 명령된 차량 감속(Commanded Vehicle Deceleration)은 예측 가능하게 유지되어야 한다.

컨택터 상태(Contactor State)는 회생 운전 중 특히 중요하다. 상당한 회생 전력이 흐르는 상태에서 메인 배터리 컨택터(Main Battery Contactor)가 개방되면 배터리로 향하는 정상적인 에너지 경로가 거의 즉시 사라진다. 남아 있는 에너지는 직류 링크 전압을 빠르게 상승시킬 수 있다. 따라서 컨택터 상태가 배터리의 분리 또는 곧 발생할 절연(Isolation)을 나타낼 때에는 회생 토크를 비활성화하거나 다른 제어 가능한 에너지 소산 경로(Controlled Dissipation Path)로 전환해야 한다.

보호 협조(Protection Coordination)는 정상적인 회생 역전류(Normal Regenerative Reverse Current)와 비정상적인 전기적 고장(Electrical Fault)을 구분해야 한다. 전류 센서(Current Sensor), 보호 알고리즘(Protection Algorithm), 컨택터, 퓨즈(Fuse), 전력 분배 장치(Power Distribution Device)는 의도된 양방향 전력 흐름(Bidirectional Power Flow)을 지원해야 한다. 전류가 항상 배터리에서 인버터 방향으로 흐른다고 가정하여 설계된 보호 시스템은 정상적인 회생 전류를 고장으로 잘못 판단하거나 역방향에서 발생하는 비정상 상태를 감지하지 못할 수 있다.

BMS와 모터 제어기 사이의 통신(Communication)은 또 다른 중요한 안전 인터페이스(Safety Interface)이다. BMS는 CAN과 같은 인터페이스를 통해 최대 충전 전류(Maximum Charging Current), 최대 충전 전력(Maximum Charging Power), SOC, 온도 상태, 전압 한계 및 고장 정보를 제공할 수 있다. 모터 제어기는 메시지 최신성(Message Freshness)과 타당성(Plausibility)을 검증해야 한다. 제한 정보가 누락되거나 지연되거나 손상되거나 비현실적인 경우에는 오래된 제한값을 계속 사용하는 대신 회생 제동을 사전에 정의된 안전 상태(Predefined Safe State)로 전환해야 한다.

셀 불균형(Cell Imbalance)은 팩 SOC가 특별히 높지 않은 경우에도 회생 충전을 제한할 수 있다. 다른 셀보다 먼저 상한 전압 임계값에 도달하는 셀이 있으면 BMS는 전체 배터리의 충전 전류를 감소시켜야 할 수 있다. 셀 밸런싱(Cell Balancing)은 사용 가능한 충전 여유(Charging Headroom)를 유지하는 데 도움이 되지만, 밸런싱 회로(Balancing Circuit)가 높은 회생 전력을 제어하는 수단을 대신할 수는 없다. 회생 제동은 항상 순간적인 셀 전압 한계(Instantaneous Cell-Voltage Limit)를 준수해야 한다.

건강 상태(SOH)는 배터리가 노화됨에 따라 회생 제동 보호에 영향을 미친다. 내부 저항(Internal Resistance)이 증가하면 동일한 충전 전류에서도 더 큰 전압 상승과 열 발생이 나타날 수 있으며, 용량 감소(Capacity Reduction)는 SOC와 셀 전압을 더 빠르게 변화시킬 수 있다. 따라서 새 배터리만을 기준으로 보정된 회생 전략(Regenerative Strategy)은 수명이 진행된 이후에는 적절하지 않을 수 있다. BMS 제한은 추정된 배터리 상태와 검증된 노화 특성(Aging Characteristics)에 맞추어 조정되어야 한다.

고장 처리(Fault Handling)는 하나의 임계값에만 의존하지 않고 계층화된 보호(Layered Protection)를 사용해야 한다. 정상 제어에서는 배터리가 운전 한계에 접근함에 따라 회생 토크를 점진적으로 디레이팅(Derating)할 수 있으며, 더 빠른 인버터 수준 보호(Inverter-Level Protection)는 과도한 직류 버스 전압이나 전류에 대응할 수 있다. BMS는 셀 수준 한계 위반에 대해 더욱 강력한 보호 동작을 수행할 수 있으며, 전기적 회생 제동을 사용할 수 없을 때에는 기계식 제동이 필요한 감속 성능을 유지할 수 있다.

자율이동로봇(AMR, Autonomous Mobile Robot)에서는 반복적인 정지-출발 운전(Stop-and-Go Operation)으로 인해 이러한 보호 메커니즘이 특히 중요하다. 빈번한 짧은 제동은 배터리에 충전 전류 펄스(Charging Pulse)를 반복적으로 유입시켜 정상적인 외부 충전(External Charging)과 다른 조건을 형성할 수 있다. 따라서 평가에서는 일반적인 충전기 프로파일(Charger Profile)만으로 배터리를 검증하지 말고 최대 회생 전류, 펄스 지속 시간(Pulse Duration), 반복 주파수(Repetition Frequency), 배터리 온도, SOC 범위, 탑재 하중(Payload), 속도 및 임무 듀티 사이클(Mission Duty Cycle)을 함께 고려해야 한다.

회생 제동 중 배터리 보호는 궁극적으로 배터리 셀, BMS, 컨택터, 직류 링크, 인버터, 모터 제어기, 제동 저항, 센서 및 기계식 제동 시스템이 함께 동작하는 통합 파워트레인 기능(Coordinated Powertrain Function)이다. 효과적인 보호 시스템은 안전 운전 경계(Safe Operating Boundary) 안에서 회수 가능한 에너지를 동적으로 극대화하는 동시에 배터리의 제한 조건이 정지 성능(Stopping Performance), 전기적 건전성(Electrical Integrity), 열 안전성(Thermal Safety), 장기 배터리 내구성(Long-Term Battery Durability)을 저해하지 않도록 해야 한다.

## 09.04. Brake Blending Control

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

브레이크 블렌딩 제어(Brake Blending Control)는 전체 요구 감속도가 부드럽고 안전하게 구현되도록 회생 제동(Regenerative Braking), 동적 제동(Dynamic Braking), 기계식 제동(Mechanical Braking)을 조정한다. 회생 제동은 운동 에너지(Kinetic Energy)를 회수할 수 있기 때문에 일반적으로 우선 적용되지만, 사용 가능한 토크는 모터 속도, 배터리 상태, 인버터 성능, 열적 한계(Thermal Limit)에 따라 지속적으로 변화한다. 블렌딩 제어는 운전자가 기대하는 제동 응답을 변화시키지 않으면서 이러한 변동을 보상한다.

기본적인 제어 목표(Control Objective)는 요구 감속도(Requested Deceleration) 또는 제동 명령(Braking Command)을 전체 제동 토크 요구량(Total Braking Torque Demand)으로 변환한 다음, 이를 사용 가능한 여러 제동 메커니즘(Braking Mechanism)에 분배하는 것이다. 회생 제동이 요구 토크 전체를 제공할 수 있다면 기계식 제동의 사용을 최소화할 수 있다. 회생 능력이 부족하면 제어기는 동일한 전체 감속 목표를 유지하면서 부족한 토크를 마찰식, 전기기계식(Electromechanical) 또는 기타 제동 장치를 통해 제공한다.

일반적인 제어 구조(Control Structure)는 운전자, 자율주행 모션 플래너(Autonomous Motion Planner), 안전 제어기(Safety Controller) 또는 속도 제어 루프(Velocity-Control Loop)에서 생성되는 제동 요구로 시작한다. 차량 질량, 휠 반경(Wheel Radius), 속도, 가속도, 경사도(Gradient), 구동계 특성(Drivetrain Characteristics)을 이용하여 필요한 휠 제동력(Wheel Braking Force)을 추정할 수 있다. 이 제동력은 액추에이터 응답(Actuator Response), 접지력(Traction), 안정성(Stability), 정지 거리 요구사항을 만족하도록 모터 및 기계식 브레이크 토크 명령으로 변환된다.

최대 회생 제동 기여도(Maximum Regenerative Contribution)는 여러 독립적인 한계에 의해 제한된다. 모터는 속도와 토크에 따라 달라지는 발전 능력(Generating Capability)을 가지며, 인버터는 전류 및 전압 한계를 갖고, 배터리에는 허용 충전 전류와 충전 전력 제한이 존재한다. 직류 링크 전압(DC-Link Voltage)과 부품 온도(Component Temperature) 역시 추가적인 제한을 발생시킨다. 따라서 브레이크 블렌딩은 제동 요구량만을 기준으로 하지 않고 현재 활성화된 제한 조건 가운데 가장 엄격한 조건을 기준으로 사용 가능한 회생 토크를 계산한다.

배터리 관리 시스템(BMS, Battery Management System)의 정보는 회생 제동 비율(Regenerative Portion)을 결정하는 데 특히 중요하다. 높은 충전 상태(SOC, State of Charge), 지나치게 낮거나 높은 온도, 셀 과전압 위험(Cell Overvoltage Risk), 저하된 건강 상태(SOH, State of Health), 충전 전류 제한은 배터리가 받아들일 수 있는 에너지를 급격하게 감소시킬 수 있다. 브레이크 제어기는 전체 제동력이 예상치 못하게 감소하지 않도록 회생 토크를 줄이는 동시에 대체 제동(Alternative Braking)의 기여도를 증가시켜야 한다.

중간 정도의 속도와 정상적인 배터리 조건에서는 회생 제동이 일반적인 감속에 필요한 제동력의 상당 부분을 제공할 수 있다. 이 운전 영역(Operating Region)은 충분한 모터 발전 전압(Motor-Generated Voltage)을 확보할 수 있고 제동 요구가 전기적 한계 내에 유지될 가능성이 높기 때문에 에너지 회수(Energy Recovery)에 가장 유리하다. 블렌딩 제어기는 회생 토크를 우선 적용하면서도 사용 가능한 전기적 제동 능력이 변화할 때 기계식 제동이 즉시 이를 보완할 수 있도록 준비 상태를 유지한다.

저속에서는 모터가 생성하는 전압과 회수 가능한 전력이 감소함에 따라 회생 토크의 효과가 점진적으로 떨어진다. 따라서 로봇이 영속도(Zero Speed)에 접근할수록 기계식 제동으로 부드럽게 전환해야 한다. 전환이 적절하게 조정되지 않으면 감속도의 급격한 변화, 정지 거리 오차(Stopping-Distance Error), 저속 진동(Low-Speed Oscillation)이 발생할 수 있다. 블렌딩 알고리즘(Blending Algorithm)은 일반적으로 회생 제동의 기여도를 점진적으로 감소시키면서 기계식 제동을 증가시켜 전체 제동 토크가 연속적으로 유지되도록 한다.

높은 감속도가 요구되는 상황에서는 반대의 문제가 발생한다. 배터리가 상당한 충전 전력을 받아들일 수 있더라도 요구되는 제동 토크가 최대 회생 능력을 초과할 수 있다. 이 경우 회생 제동은 안전한 한계 범위에서 동작하고, 기계식 제동이 추가적으로 필요한 토크를 제공해야 한다. 비상 제동(Emergency Braking)에서는 에너지 회수보다 정지 성능과 안전을 우선해야 하므로 회생 에너지 최적화(Regenerative Optimization)가 필요한 제동 응답을 지연시키거나 감소시켜서는 안 된다.

동적 제동(Dynamic Braking)은 회생 전기 토크를 생성할 수 있지만 배터리가 생성된 에너지를 받아들일 수 없을 때 또 다른 블렌딩 경로를 제공한다. 제동 초퍼(Braking Chopper)와 제동 저항(Braking Resistor)은 초과 직류 링크 에너지를 열로 소산하면서 전기적 제동을 지속할 수 있게 한다. 따라서 제어기는 배터리 제한, 직류 버스 전압(DC-Bus Voltage), 열 용량(Thermal Capacity), 요구 감속도에 따라 배터리 회생(Battery Regeneration), 저항 기반 동적 제동(Resistor-Based Dynamic Braking), 기계식 제동 사이에서 제동력을 분배할 수 있다.

토크 블렌딩(Torque Blending)은 액추에이터 동특성(Actuator Dynamics)의 차이를 고려해야 한다. 모터 토크는 일반적으로 인버터 전류 제어(Inverter Current Control)를 통해 빠르게 변경할 수 있지만, 기계식 브레이크는 액추에이터 움직임, 압력 형성(Pressure Buildup), 간극(Clearance), 컴플라이언스(Compliance) 때문에 상대적으로 느린 응답을 나타낼 수 있다. 기계식 토크가 형성되기 전에 회생 토크를 제거하면 일시적인 제동력 부족이 발생할 수 있고, 반대로 지나치게 많이 중첩되면 원하지 않는 감속 피크(Deceleration Peak)가 발생할 수 있으므로 전환 시점(Transition Timing)은 중요한 보정 파라미터(Calibration Parameter)가 된다.

피드포워드 제어(Feedforward Control)와 피드백 제어(Feedback Control)를 결합하여 블렌딩 정확도를 향상시킬 수 있다. 피드포워드 로직(Feedforward Logic)은 요구 감속도와 알려진 차량 파라미터를 이용하여 필요한 토크를 추정하고, 피드백은 측정된 휠 속도, 차량 속도, 가속도, 모터 토크 또는 기타 신호를 사용하여 오차를 보정한다. 이러한 조합은 실제 운전 중 탑재 하중 변화, 경사도, 구동계 손실, 타이어 상태 및 기계식 브레이크 동작 변화에 대한 보상을 가능하게 한다.

자율이동로봇(AMR, Autonomous Mobile Robot)은 공차 상태(Empty Vehicle Mass)에 비해 탑재 하중(Payload)의 변화가 상당히 클 수 있다. 따라서 동일한 요구 감속도를 구현하더라도 운반 중인 하중에 따라 필요한 제동력이 달라진다. 추정 또는 측정된 총중량(Gross Mass)을 사용하는 블렌딩 제어기는 제동 토크를 더욱 정확하게 분배할 수 있다. 질량 보상(Mass Compensation)이 없다면 고정된 토크 명령은 무부하 상태와 최대 적재 상태 사이에서 서로 다른 정지 거리를 발생시킬 수 있다.

휠 접지력(Wheel Traction) 역시 사용할 수 있는 회생 제동을 제한한다. 마찰계수가 낮은 노면(Low-Friction Surface)에서 과도한 음의 모터 토크(Negative Motor Torque)를 적용하면 특히 강한 감속이나 젖은 노면, 먼지가 많은 노면, 결빙 노면 또는 불규칙한 지형에서 휠 슬립(Wheel Slip)이나 방향 안정성(Direction Stability) 저하가 발생할 수 있다. 휠 속도 정보, 관성 측정값(Inertial Measurement), 접지력 추정값(Traction Estimate)을 이용하여 명령 제동 토크를 감소시킬 수 있으며, 타이어-노면 접착력(Tire-Ground Adhesion)이 안전한 제동력을 제한하는 경우 에너지 회수는 부차적인 목표가 된다.

추진(Propulsion)에서 제동으로 전환하는 과정 역시 세심하게 관리해야 한다. 양의 모터 토크(Positive Motor Torque)에서 강한 음의 토크로 급격하게 반전하면 구동계 충격(Drivetrain Shock), 전류 과도 현상(Current Transient), 불편하거나 불안정한 차량 움직임이 발생할 수 있다. 토크 변화율 제한(Torque-Rate Limiting), 필터링(Filtering), 데드밴드 관리(Deadband Management), 저크 제어(Jerk Control)를 통해 이러한 전환을 조정할 수 있다. 정밀 자율이동로봇에서는 급격한 종방향 운동(Longitudinal Motion)이 탑재물 안정성과 위치추정 정확도(Localization Accuracy)에 영향을 줄 수 있기 때문에 제어된 저크가 특히 중요하다.

고장 상태(Fault Condition)에 대해서는 사전에 정의된 성능 저하 전략(Degradation Strategy)이 필요하다. BMS 통신 손실, 인버터 고장, 과도한 직류 링크 전압, 모터 온도 제한, 컨택터 개방(Contactor Opening), 센서 고장은 회생 제동을 감소시키거나 완전히 제거할 수 있다. 블렌딩 제어기는 남아 있는 제동 능력을 판단하여 요구 토크를 기계식 또는 기타 사용 가능한 제동 시스템으로 전달해야 한다. 에너지 회수 경로(Energy-Recovery Path)의 고장이 필요한 감속을 달성하지 못하는 제동 기능의 고장으로 이어져서는 안 된다.

기계식 브레이크 상태(Mechanical Brake Condition) 역시 고려해야 한다. 회생 제동을 빈번하게 사용하면 일반적인 마찰 브레이크(Friction Brake)의 사용 빈도가 감소한다. 이는 패드(Pad)나 라이닝(Lining)의 수명을 연장할 수 있지만, 장기간 기계식 제동을 제한적으로 사용하면 마찰면 상태, 액추에이터 준비 상태(Actuator Readiness), 제동 일관성(Braking Consistency)에 영향을 줄 수 있다. 필요한 경우 주기적인 브레이크 작동(Brake Exercise) 또는 진단 루틴(Diagnostic Routine)을 적용하여 회생 제동이 제한되거나 비상 정지가 필요한 상황에서도 기계식 제동 시스템을 정상적으로 사용할 수 있도록 유지할 수 있다.

브레이크 블렌딩 보정(Brake Blending Calibration)은 단순히 고정된 회생 제동 비율을 선택하는 것 이상을 요구한다. 엔지니어는 모터 속도, 배터리 SOC, 온도, 직류 버스 전압, 탑재 하중, 경사도 및 제동 요구량에 따른 회생 토크 능력(Regenerative Torque Capability)을 특성화해야 한다. 전환 임계값(Transition Threshold), 토크 램프(Torque Ramp), 액추에이터 지연(Actuator Delay), 저속 전환(Low-Speed Handover), 고장 대응 및 기계식 브레이크 보상은 단일 기준 시험 조건이 아니라 대표적인 실제 운전 조건 전체에서 검증되어야 한다.

성능 평가(Performance Evaluation)에서는 전체 정지 거리, 감속 추종(Deceleration Tracking), 저크(Jerk), 회생 에너지, 직류 링크 안정성(DC-Link Stability), 배터리 전류, 휠 슬립, 전환 품질(Transition Quality)을 평가해야 한다. 자율이동로봇에서는 하나의 임무 동안 제어기가 추진과 제동 사이를 수천 번 전환할 수 있기 때문에 반복적인 정지-출발 사이클(Stop-and-Go Cycle)이 특히 중요하다. 열 축적(Thermal Accumulation)과 변화하는 SOC는 회생 능력을 점진적으로 변화시킬 수 있으므로 전체 듀티 사이클(Duty Cycle) 동안 일관된 블렌딩 동작을 유지해야 한다.

따라서 브레이크 블렌딩 제어(Brake Blending Control)는 변화하는 전기적 및 기계적 제동 능력을 예측 가능한 차량 감속으로 변환하는 핵심 조정 계층(Coordination Layer)이다. 회생 토크, 동적 에너지 소산(Dynamic Dissipation), 기계식 제동을 지속적으로 균형 있게 조절함으로써 배터리, 인버터, 모터, 접지력 또는 열적 한계를 위반하지 않으면서 에너지 회수를 극대화할 수 있다. 효과적인 블렌딩은 로봇 파워트레인(Robotic Powertrain)에 부드러운 정지, 안정적인 직류 버스 동작, 고장 허용성(Fault Tolerance), 신뢰할 수 있는 제동 성능을 제공한다.

## 09.05. Regen for AMR and UAV

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

자율이동로봇(AMR, Autonomous Mobile Robot)과 무인항공기(UAV, Unmanned Aerial Vehicle)의 회생 제동(Regenerative Braking)은 근본적으로 서로 다른 운동 및 에너지 특성을 고려하여 설계해야 한다. AMR은 감속 과정에서 구동 휠(Driven Wheel)을 통해 병진 및 회전 운동 에너지(Translational and Rotational Kinetic Energy)를 직접 회수할 수 있는 반면, UAV는 주로 회전하는 프로펠러(Propeller)와 공기역학적 힘(Aerodynamic Force)을 통해 에너지를 교환한다. 동일한 양방향 모터 드라이브 원리(Bidirectional Motor-Drive Principle)가 적용되지만 실제 에너지 회수 기회는 크게 다르다.

AMR에서 회생 제동은 구동계(Traction Drivetrain)에 자연스럽게 통합된다. 로봇이 감속하면 휠의 회전이 BLDC 또는 영구자석 동기 모터(PMSM, Permanent Magnet Synchronous Motor)를 발전 운전(Generating Operation) 상태로 구동한다. 전기 에너지는 3상 인버터(Three-Phase Inverter)와 직류 링크(DC Link)를 통해 배터리 방향으로 흐른다. 휠은 지면의 움직임과 직접적인 기계적 관계를 유지하므로 명령된 음의 모터 토크(Negative Motor Torque)는 차량 제동과 회수 가능한 전력 생성을 동시에 수행한다.

AMR은 가속, 정속 주행(Cruising), 감속, 정지를 반복하는 운전 사이클을 빈번하게 수행한다. 창고 운송, 공장 물류, 검사, 순찰, 실외 배송 임무에는 수백 번 또는 수천 번의 제동 이벤트(Braking Event)가 포함될 수 있다. 각각의 제동에서 회수되는 에너지는 크지 않을 수 있지만 누적된 에너지는 순 추진 에너지 소비(Net Propulsion Consumption)를 감소시키고 배터리 방전 깊이(Depth of Discharge)를 줄이며 충전 사이의 운전 시간을 잠재적으로 연장할 수 있다.

탑재 하중(Payload)은 전체 이동 질량이 증가함에 따라 운동 에너지가 증가하기 때문에 AMR의 회생 제동에 큰 영향을 미친다. 동일한 속도로 주행하는 경우 무거운 하중을 탑재한 로봇은 무부하 로봇보다 이론적으로 제동 중 회수할 수 있는 에너지가 더 많다. 그러나 높은 질량은 필요한 제동 토크와 최대 회생 전력(Peak Regenerative Power)도 증가시킨다. 따라서 모터, 인버터, 배터리, 구동계 및 기계식 브레이크(Mechanical Brake)는 예상되는 최대 총중량 조건(Maximum Gross Vehicle Condition)을 기준으로 용량을 선정해야 한다.

실외 자율이동로봇(Outdoor AMR)은 지형 경사(Terrain Gradient)를 통해 추가적인 회생 에너지 기회를 얻을 수 있다. 내리막 주행 중에는 중력 위치 에너지(Gravitational Potential Energy)가 지속적으로 차량을 움직이며, 회생 토크가 속도를 제어하는 동안 이를 전기 에너지로 변환할 수 있다. 긴 내리막에서는 회생 운전이 장시간 지속될 수 있기 때문에 개별 정지보다 더 가혹한 조건이 발생할 수 있으며, 배터리 충전 수용 능력(Battery Charge Acceptance), 인버터 온도, 모터 온도 및 직류 버스 제어(DC-Bus Regulation)가 중요한 연속 전력 제한(Continuous-Power Constraint)이 된다.

매우 낮은 속도에서는 모터가 생성하는 전압과 이용 가능한 전력이 감소함에 따라 AMR의 회생 제동 능력(Regenerative Capability)이 저하된다. 따라서 최종 정지, 정지 상태 유지(Stationary Holding), 비상 제동(Emergency Braking), 배터리가 에너지를 받아들일 수 없는 상황에서는 기계식 또는 전기기계식 제동(Electromechanical Braking)이 필요하다. 브레이크 블렌딩 제어(Brake Blending Control)는 변화하는 운전 조건에서도 정지 거리와 감속도가 예측 가능하도록 회생 제동과 기계식 제동 사이에서 토크를 점진적으로 전환해야 한다.

접지 조건(Traction Condition) 역시 AMR의 회생 제동을 제한한다. 과도한 음의 휠 토크(Negative Wheel Torque)는 젖거나 먼지가 많거나 결빙되거나 느슨하거나 불규칙한 노면에서 슬립(Slip)을 발생시킬 수 있다. 따라서 제어 시스템은 회생 토크를 휠 속도 감지(Wheel-Speed Sensing), 차량 속도 추정(Vehicle-Speed Estimation), 관성 측정(Inertial Measurement), 가용 마찰력(Available Friction)과 연계하여 조정해야 한다. 최대 에너지 회수보다 모바일 플랫폼의 방향 안정성(Direction Stability), 제어 가능성(Controllability), 요구 정지 성능을 유지하는 것이 우선한다.

UAV의 회생 에너지 회수는 지속적으로 추진 모터를 구동할 수 있는 휠-지면 인터페이스(Wheel-Ground Interface)가 일반적으로 존재하지 않기 때문에 AMR과 다른 공학적 문제를 갖는다. 일반적인 동력 비행(Powered Flight)에서는 프로펠러가 공기역학적 추력(Aerodynamic Thrust)을 발생시키기 위해 전기 에너지를 소비한다. 에너지를 회수하려면 공기 흐름이 프로펠러 또는 로터(Rotor)를 충분히 강하게 구동하여 연결된 모터가 발전기로 동작하고 유용한 전력을 직류 시스템으로 반환할 수 있는 공기역학적 조건이 필요하다.

하강 비행(Descending Flight)은 UAV 에너지 회수를 위한 하나의 가능한 기회를 제공한다. 공기역학 및 로터 운전 조건이 윈드밀링(Windmilling) 또는 자동회전(Autorotative Behavior)을 허용한다면 로터를 통과하는 공기 흐름이 모터-발전기(Motor-Generator)에 기계 동력을 제공할 수 있다. 인버터는 양방향 운전(Bidirectional Operation)을 지원해야 하며 비행 제어기(Flight Controller)는 로터 속도, 발전 토크, 추력 및 기체 안정성을 동시에 제어해야 한다. 따라서 회수 가능한 에너지는 항공기 및 추진 시스템 아키텍처에 크게 의존한다.

모든 멀티로터 UAV(Multirotor UAV)에서 회생 운전이 유리하다고 가정해서는 안 된다. 일반적인 멀티로터는 하강 중에도 자세 제어(Attitude Control)와 비행 안정성(Flight Stability)을 추진 시스템이 담당하기 때문에 상당한 로터 추력이 필요하다. 로터를 강제로 높은 발전 운전 상태로 전환하면 추력과 공기역학적 거동이 변화할 수 있다. 따라서 회수되는 에너지는 제어된 비행을 유지하기 위해 필요한 에너지와 비교할 때 매우 작을 수 있다.

고정익(Fixed-Wing) 또는 하이브리드 수직이착륙(Hybrid VTOL, Vertical Take-Off and Landing) 구성은 공기역학적 양력(Aerodynamic Lift)이 항공기를 지지하는 동안 일부 추진 장치가 유리한 공기 흐름을 받을 수 있기 때문에 다른 회생 가능성을 제공한다. 하강, 감속 또는 특정 비행 단계에서 양방향 전력 변환을 위해 설계된 프로펠러가 공중 터빈(Airborne Turbine)처럼 동작할 수 있다. 실제 임무에서 순수한 이점이 발생하는지는 프로펠러 형상, 비행 속도, 항력(Drag), 모터 효율, 인버터 효율 및 추가 하드웨어의 질량에 따라 달라진다.

대형 화물 UAV(Cargo UAV)는 추진 전력이 매우 높을 수 있기 때문에 특히 세심한 검토가 필요하다. 짧은 발전 운전에서도 상당한 전력이 발생할 수 있으며, 이를 직류 버스와 배터리가 수용할 수 있어야 한다. 따라서 배터리 SOC, 셀 전압, 온도, 충전 전류 능력, 컨택터 상태(Contactor State), 열적 조건(Thermal Condition)을 기준으로 회생 명령을 제한해야 한다. 그렇지 않으면 과도한 발전 전력으로 직류 링크 과전압(DC-Link Overvoltage)이나 과도한 배터리 충전 전류가 빠르게 발생할 수 있다.

하이브리드 UAV 파워트레인(Hybrid UAV Powertrain)은 추가적인 에너지 관리 가능성을 제공한다. 배터리, 발전기(Generator), 엔진 구동 전원(Engine-Driven Power Source), 다수의 추진 인버터, 직류 배전 네트워크(DC Distribution Network)가 하나의 전기 아키텍처를 공유할 수 있다. 회수된 에너지는 탑재 전기 부하(Onboard Electrical Load)를 공급하거나 배터리를 충전하거나 발전기 출력을 감소시키는 데 사용할 수 있다. 상위 에너지 관리(Supervisory Energy Management)는 직류 버스 안정성을 유지하고 연결된 모든 전원의 운전 한계를 준수하면서 적절한 에너지 전달 대상을 결정해야 한다.

제어 목표(Control Objective) 역시 지상 플랫폼과 공중 플랫폼에서 서로 다르다. AMR에서는 음의 구동 토크(Negative Traction Torque)가 종방향 감속(Longitudinal Deceleration)과 직접적으로 연결되므로 회생 제동은 모션 제어(Motion Control)의 자연스러운 구성 요소가 된다. 반면 UAV에서는 모터 토크가 주로 로터 속도와 추력을 결정하고, 이는 양력(Lift), 자세 및 안정성에 직접적인 영향을 미친다. 따라서 회생 운전은 비행 제어 권한(Flight-Control Authority)에 종속되어야 하며 독립적인 에너지 회수 기능으로 최적화해서는 안 된다.

고장 처리(Failure Handling)에서도 이러한 차이가 나타난다. AMR에서 회생 제동 기능이 상실되더라도 충분히 독립적인 제동 능력이 있다면 일반적으로 기계식 제동으로 보완할 수 있다. UAV에서는 구동 운전(Motoring State)과 발전 운전(Generating State) 사이의 부적절한 전환이 추력 생성에 직접 영향을 미칠 수 있다. 따라서 비행 필수 추진 제어(Flight-Critical Propulsion Control)는 에너지 회수를 시도하기 전에 필요한 로터 추력과 안정성을 우선적으로 보장해야 하며, 안전한 비행 제어 요구사항과 충돌하는 경우 회생 운전을 금지해야 한다.

배터리 보호(Battery Protection)는 두 응용 분야 모두에 공통적으로 적용된다. BMS는 SOC, 개별 셀 전압, 전류, 온도, 건강 상태(SOH, State of Health), 고장 조건을 기반으로 동적 충전 한계(Dynamic Charging Limit)를 제공해야 한다. 모터 제어기 또는 상위 전력 제어기(Supervisory Power Controller)는 이러한 한계를 허용 가능한 회생 전력으로 변환한다. 배터리가 에너지를 받아들일 수 없는 경우 회생 운전을 감소시키거나 다른 부하 또는 저장 경로로 전환하거나 적절하게 설계된 전기적 메커니즘을 통해 에너지를 소산해야 한다.

효율(Efficiency)은 모터-발전기만을 기준으로 평가하기보다 임무 수준(Mission Level)에서 평가해야 한다. AMR의 이점은 차량 질량, 속도 프로파일(Speed Profile), 제동 빈도, 경사도, 보조 부하(Auxiliary Load), 기계식 제동 요구사항에 따라 달라진다. UAV의 이점은 추가적으로 공기역학적 손실(Aerodynamic Penalty), 로터 거동, 비행 궤적(Flight Trajectory), 추진 시스템 아키텍처, 추가되는 컨버터 또는 제어 하드웨어의 영향을 받는다. 높은 전기 변환 효율(Electrical Conversion Efficiency)이 반드시 전체 임무 지속시간의 의미 있는 향상을 보장하는 것은 아니다.

따라서 AMR에서 회생 제동은 이미 양방향으로 동작하는 전기 구동 시스템(Bidirectional Electric Traction System)을 실용적으로 확장한 기능이며 일반적으로 높은 활용 가치를 가진다. 반복적인 정지와 내리막 주행에서 기존에 소산되던 에너지의 일부를 회수하면서 기계식 브레이크 사용을 감소시킬 수 있다. 적절한 모터 용량 선정, 인버터 제어, 배터리 충전 수용 능력, 접지력 관리(Traction Management), 브레이크 블렌딩, 임무별 보정(Mission-Specific Calibration)을 통해 효과를 극대화할 수 있다.

반면 UAV의 회생 운전은 보편적으로 적용 가능한 제동 기능이 아니라 아키텍처 의존적 기회(Architecture-Dependent Opportunity)로 다루어야 한다. 필요한 추력이나 안정성을 저해하지 않으면서 공기역학적 에너지가 자연스럽게 로터 또는 프로펠러를 구동할 수 있는 경우에 가장 현실적인 적용 가능성을 갖는다. 하이브리드 및 특수 항공기 구성은 유용한 운전 영역을 제공할 수 있지만 실제 효과는 추진, 공기역학, 배터리 및 임무 수준 분석을 통해 검증해야 한다.

전체적인 설계 원칙(Design Principle)은 에너지 회수가 주요 운동 목표(Primary Motion Objective)를 저해하지 않고 지원할 수 있을 때에만 에너지를 회수하는 것이다. AMR은 안정적인 감속과 정지를 우선하고, UAV는 추력, 자세 및 비행 안전(Flight Safety)을 우선한다. 두 플랫폼 모두에서 모터, 인버터, 직류 버스, 배터리, BMS 기능, 열 관리 시스템(Thermal System), 상위 제어기(Supervisory Controller) 사이의 협조 제어를 통해 안전한 전기적 및 동적 운전 경계(Safe Electrical and Dynamic Operating Boundary) 안에서 회생 에너지를 회수할 수 있다.
