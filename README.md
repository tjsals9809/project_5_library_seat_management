# 📚 Project_5 Library Seat Management 💺

## 📌 1. Project Summary (프로젝트 요약)

Basys3 FPGA 보드와 Vivado Block Design을 기반으로 구현한 **도서관 좌석 관리 시스템**입니다.

MicroBlaze RISC-V 프로세서를 중심으로 AXI GPIO, AXI UARTLite, AXI Timer, AXI Quad SPI를 연결하여 LCD 출력, SPI 기반 외부 모듈 통신, UART 디버깅이 가능한 임베디드 시스템 구조를 구성했습니다. 도서관 좌석의 사용 상태를 확인하고, 좌석 이용/반납 과정을 관리할 수 있도록 하드웨어 플랫폼을 설계했습니다.

---

## ✨ 2. Key Features (주요 기능)

### 2.1 📚 Library Seat Status Management (도서관 좌석 상태 관리)

  * 도서관 좌석의 사용 가능 여부를 관리하는 시스템 구조
  * 좌석 사용, 반납, 상태 확인 흐름을 임베디드 시스템으로 구성
  * 좌석 상태 정보를 LCD 화면에 표시할 수 있도록 출력부 구성

### 2.2 💺 Seat Check-In / Check-Out Control (좌석 이용·반납 제어)

  * 좌석 이용 등록과 반납 처리를 위한 기본 제어 구조 구현
  * 사용자 입력 또는 외부 모듈 입력을 통해 좌석 상태 변경 가능
  * 좌석이 사용 중인지, 비어 있는지 확인할 수 있는 흐름 구성

### 2.3 🖥️ LCD Display Output (LCD 화면 출력)

  * AXI GPIO를 이용해 LCD 제어 신호 출력
  * 6bit LCD 제어 버스를 통해 문자 LCD와 연결
  * 좌석 상태, 안내 문구, 오류 메시지 등을 표시할 수 있는 출력 구조 구성

### 2.4 🔐 SPI External Module Interface (SPI 외부 모듈 연동)

  * AXI Quad SPI IP를 사용하여 SPI 기반 외부 장치와 통신
  * RFID, 센서, 기타 SPI 모듈을 연결할 수 있는 확장 구조
  * `spi_rtl_0` 포트를 통해 `SS`, `SCK`, `MOSI`, `MISO` 신호 사용

### 2.5 🔁 Timer-based System Control (타이머 기반 제어)

  * AXI Timer를 이용해 일정 시간 간격의 이벤트 처리 가능
  * LCD 갱신, 좌석 상태 유지 시간 계산, 주기적 상태 확인 등에 활용 가능
  * 시간 기반 동작을 하드웨어 타이머로 안정적으로 처리

### 2.6 🧩 MicroBlaze RISC-V based Embedded System (MicroBlaze RISC-V 기반 임베디드 시스템)

  * Vivado Block Design에서 MicroBlaze RISC-V 프로세서 사용
  * AXI SmartConnect를 통해 UART, GPIO, Timer, SPI IP를 하나의 시스템으로 연결
  * Vitis와 연동하여 C 기반 소프트웨어 제어가 가능한 하드웨어 플랫폼 구성

---

## ⚙️ 3. Tech Stack (기술 스택)

### 3.1 Language / Design

<p>
  <img src="https://img.shields.io/badge/Verilog-HDL-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Block%20Design-Vivado-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/C-Vitis-blue?style=for-the-badge">
</p>

### 3.2 Hardware / IP

<p>
  <img src="https://img.shields.io/badge/Basys3-FPGA-red?style=for-the-badge">
  <img src="https://img.shields.io/badge/MicroBlaze-RISC--V-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/AXI-GPIO-yellow?style=for-the-badge">
  <img src="https://img.shields.io/badge/AXI-UARTLite-lightgrey?style=for-the-badge">
  <img src="https://img.shields.io/badge/AXI-Quad%20SPI-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/AXI-Timer-black?style=for-the-badge">
</p>

### 3.3 Development Environment (개발 환경)

<p>
  <img src="https://img.shields.io/badge/Xilinx-Vivado-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/AMD-Vitis-red?style=for-the-badge">
  <img src="https://img.shields.io/badge/Ubuntu-24.04-purple?style=for-the-badge">
</p>

---

## 🗂️ 4. Project Structure (프로젝트 구조)

### Project Tree (프로젝트 트리)

```txt
project_LIBRARY/
├── project_LIBRARY.xpr                          # Vivado 프로젝트 파일
├── design_library_wrapper.xsa                   # Vitis 연동용 하드웨어 플랫폼 파일
│
├── project_LIBRARY.srcs/
│   ├── sources_1/
│   │   └── bd/
│   │       └── design_library/
│   │           ├── design_library.bd            # Vivado Block Design
│   │           └── ip/                          # MicroBlaze 및 AXI IP 설정
│   │
│   └── constrs_1/
│       └── imports/
│           └── fpga/
│               └── Basys-3-Master.xdc           # Basys3 핀 제약 조건
│
├── project_LIBRARY.gen/
│   └── sources_1/
│       └── bd/
│           └── design_library/
│               ├── hdl/
│               │   └── design_library_wrapper.v # Block Design Wrapper
│               └── ip/                          # 생성된 IP HDL 파일
│
├── project_LIBRARY.runs/
│   ├── synth_1/                                 # 합성 결과
│   └── impl_1/                                  # 구현 및 bitstream 결과
│       ├── design_library_wrapper.bit           # FPGA 업로드용 bitstream
│       └── design_library_wrapper.mmi
│
├── project_LIBRARY.hw/                          # Hardware Manager 관련 파일
├── project_LIBRARY.sim/                         # 시뮬레이션 관련 파일
└── README.md                                    # 프로젝트 설명 문서
```

---

## 🧱 5. System Design (시스템 설계)

### 5.1 Hardware Block Diagram (하드웨어 블록다이어그램)

```mermaid
flowchart LR
    CLK[100MHz Clock] --> CLK_WIZ[Clock Wizard]
    RESET[Reset Button] --> RST[Processor System Reset]

    CLK_WIZ --> MB[MicroBlaze RISC-V]
    RST --> MB

    MB --> AXI[AXI SmartConnect]

    AXI --> UART[AXI UARTLite]
    AXI --> GPIO[AXI GPIO LCD]
    AXI --> TIMER[AXI Timer]
    AXI --> SPI[AXI Quad SPI]

    UART --> PC[PC Serial Monitor]
    GPIO --> LCD[Character LCD]
    TIMER --> TIME[Seat Time / Refresh Control]
    SPI --> EXT[SPI External Module]

    EXT --> RFID[RFID / Sensor Module]
    LCD --> USER[Seat Status Display]
```

---

### 5.2 System Flow Chart (동작 흐름도)

```mermaid
flowchart TD
    A[System Start] --> B[Hardware Initialize]
    B --> C[LCD Initialize]
    C --> D[SPI / UART / Timer Initialize]
    D --> E[Idle State]

    E --> F{User Input or Card Tag?}
    F -- No --> E
    F -- Yes --> G{Seat Available?}

    G -- Yes --> H[Seat Check-In]
    H --> I[Update Seat State]
    I --> J[Display Seat Info on LCD]
    J --> E

    G -- No --> K[Display Full / Error Message]
    K --> E

    E --> L{Return Request?}
    L -- Yes --> M[Seat Check-Out]
    M --> N[Clear Seat State]
    N --> O[Display Return Complete]
    O --> E
```

---

## 🔌 6. I/O Control (입출력 제어)

| Input / Output | Function |
|---|---|
| `sys_clock` | Basys3 100MHz 시스템 클럭 |
| `reset` | 시스템 리셋 입력 |
| `lcd_bus_tri_o[5:0]` | LCD 제어 및 데이터 출력 |
| `spi_rtl_0_ss_io[0]` | SPI Slave Select |
| `spi_rtl_0_sck_io` | SPI Clock |
| `spi_rtl_0_io0_io` | SPI 데이터 신호 |
| `spi_rtl_0_io1_io` | SPI 데이터 신호 |
| `usb_uart_rxd` | UART 수신 |
| `usb_uart_txd` | UART 송신 |

---

## 🧩 7. Main IP Blocks (주요 IP 구성)

### 7.1 `microblaze_riscv_0`

시스템의 중앙 제어를 담당하는 프로세서입니다.

주요 역할:

  * LCD 출력 제어
  * SPI 외부 모듈 통신 제어
  * UART를 통한 디버깅 메시지 송수신
  * 좌석 상태 관리 로직 수행

---

### 7.2 `axi_gpio_lcd`

LCD와 연결되는 GPIO 출력 IP입니다.

주요 역할:

  * 6bit LCD 제어 신호 출력
  * LCD 명령어 및 데이터 전달
  * 좌석 상태 메시지 표시

---

### 7.3 `axi_quad_spi_0`

SPI 기반 외부 모듈과 통신하기 위한 IP입니다.

주요 역할:

  * SPI Clock, Slave Select, Data 신호 제어
  * RFID 또는 SPI 센서 모듈과의 통신 구조 제공
  * 사용자 인식 또는 외부 입력 확장에 활용

---

### 7.4 `axi_uartlite_0`

PC와 UART 통신을 수행하는 IP입니다.

주요 역할:

  * 시리얼 모니터를 통한 디버깅 출력
  * 시스템 상태 메시지 확인
  * 좌석 등록/반납 과정 확인

---

### 7.5 `axi_timer_0`

시간 기반 제어를 담당하는 IP입니다.

주요 역할:

  * LCD 갱신 주기 관리
  * 좌석 이용 시간 계산
  * 주기적 상태 확인 이벤트 생성

---

### 7.6 `axi_smc`

MicroBlaze RISC-V와 여러 AXI 주변장치를 연결하는 SmartConnect IP입니다.

주요 역할:

  * AXI UARTLite, AXI GPIO, AXI Timer, AXI Quad SPI 연결
  * 주소 기반 주변장치 접근 지원
  * MicroBlaze 중심의 시스템 버스 구성

---

## 🗺️ 8. Address Map (주소 맵)

| Peripheral | Base Address | Range |
|---|---:|---:|
| AXI GPIO LCD | `0x40000000` | `64K` |
| AXI UARTLite | `0x40600000` | `64K` |
| AXI Timer | `0x41C00000` | `64K` |
| AXI Quad SPI | `0x44A00000` | `64K` |
| Local Memory | `0x00000000` | `128K` |

---

## 🧭 9. Operation Flow (동작 흐름)

### 9.1 Seat Check-In (좌석 이용 등록)

```txt
1. 시스템 전원 인가
2. MicroBlaze RISC-V 초기화
3. LCD, UART, Timer, SPI 초기화
4. 사용자 입력 또는 외부 모듈 입력 대기
5. 좌석 사용 가능 여부 확인
6. 사용 가능한 좌석이 있으면 좌석 배정
7. 좌석 상태를 사용 중으로 변경
8. LCD에 좌석 이용 안내 문구 출력
9. UART로 현재 상태 디버깅 출력
```

---

### 9.2 Seat Check-Out (좌석 반납)

```txt
1. 반납 입력 또는 사용자 인식
2. 현재 사용 중인 좌석 정보 확인
3. 해당 좌석 상태를 빈자리로 변경
4. LCD에 반납 완료 문구 출력
5. 좌석 상태 갱신
6. 다음 사용자 입력 대기
```

---

### 9.3 Error Handling (오류 처리)

```txt
1. 사용 가능한 좌석이 없는 경우
2. 이미 사용 중인 좌석을 다시 선택한 경우
3. 등록되지 않은 사용자 정보가 입력된 경우
4. SPI 외부 모듈 통신이 정상적으로 이루어지지 않는 경우
5. LCD 출력이 초기화되지 않은 경우
6. 오류 메시지를 LCD 또는 UART로 출력
```

---

## 🖼️ 10. Image Preview (이미지)

### 10.1 Final Product (완성품)

<p>
  <img src="./images/library_seat.jpg" alt="Library Seat Final Product" width="500">
</p>

### 10.2 LCD Display (LCD 출력 화면)

<p>
  <img src="./images/lcd_display.jpg" alt="LCD Display" width="500">
</p>

### 10.3 Vivado Block Design (Vivado 블록 디자인)

<p>
  <img src="./images/block_design.jpg" alt="Vivado Block Design" width="700">
</p>

---

## 🎬 11. Demonstration (시연 영상)

### 이미지를 클릭하면 영상으로 이동합니다

<p>
  <a href="https://www.youtube.com/watch?v=YOUR_VIDEO_ID">
    <img src="./images/youtube.png" alt="YouTube Demo" width="120">
  </a>
</p>

---

## 🛠️ 12. Troubleshooting (문제 해결 기록)

### 12.1 LCD 출력 핀 연결 문제

**🔍 문제 상황**

  * LCD에 문자가 출력되지 않거나, 화면에 깨진 문자가 표시되는 문제가 발생했습니다.

**❓ 원인 분석**

  * LCD 제어 신호와 Basys3 보드의 PMOD 핀 연결이 정확히 맞지 않으면 데이터가 정상적으로 전달되지 않습니다.
  * Vivado의 XDC 파일에서 `lcd_bus_tri_o[5:0]` 신호와 실제 LCD 연결 핀을 일치시켜야 했습니다.

**❗ 해결 방법**

  * `Basys-3-Master.xdc` 파일에서 LCD에 사용하는 PMOD 핀만 활성화했습니다.
  * `lcd_bus_tri_o[5:0]` 신호를 JB 포트에 연결하여 LCD 제어 신호가 정상적으로 출력되도록 수정했습니다.

**✅ 결과**

  * LCD에 좌석 상태와 안내 메시지가 정상적으로 출력되었습니다.
  * 하드웨어 핀 연결과 Vivado 제약 조건을 일치시키는 과정의 중요성을 확인했습니다.

---

### 12.2 SPI 외부 모듈 통신 문제

**🔍 문제 상황**

  * SPI 기반 외부 모듈과 통신할 때 데이터가 정상적으로 읽히지 않는 문제가 발생했습니다.

**❓ 원인 분석**

  * SPI 통신은 `SS`, `SCK`, 데이터 입출력 신호가 정확히 연결되어야 합니다.
  * SPI 모드와 클럭 설정이 외부 모듈과 맞지 않으면 데이터 송수신이 실패할 수 있습니다.

**❗ 해결 방법**

  * AXI Quad SPI IP를 추가하고, `spi_rtl_0` 인터페이스를 외부 포트로 연결했습니다.
  * XDC 파일에서 JA 포트에 SPI 신호를 할당했습니다.
  * SPI 모드와 Slave Select 사용 방식을 확인하여 외부 모듈과 통신할 수 있도록 구성했습니다.

**✅ 결과**

  * SPI 외부 장치를 연결할 수 있는 하드웨어 인터페이스가 구성되었습니다.
  * 좌석 관리 시스템에 RFID 또는 센서 모듈을 확장할 수 있는 기반을 마련했습니다.

---

### 12.3 UART 디버깅 연결 문제

**🔍 문제 상황**

  * 시스템 상태를 확인하기 위해 UART 출력을 사용했지만, PC 시리얼 모니터에서 값이 정상적으로 보이지 않는 문제가 발생했습니다.

**❓ 원인 분석**

  * UART 통신은 보드의 RX/TX 핀 설정과 Baud Rate가 맞아야 정상적으로 출력됩니다.
  * AXI UARTLite의 Baud Rate와 PC 시리얼 모니터 설정이 다르면 문자가 깨져 보일 수 있습니다.

**❗ 해결 방법**

  * AXI UARTLite IP를 추가하고 `usb_uart_rxd`, `usb_uart_txd` 포트를 외부로 연결했습니다.
  * Baud Rate를 `115200`으로 설정하고, PC 시리얼 모니터도 동일한 값으로 맞췄습니다.

**✅ 결과**

  * UART를 통해 시스템 상태와 디버깅 메시지를 확인할 수 있게 되었습니다.
  * LCD만으로 확인하기 어려운 내부 동작 상태를 PC에서 확인할 수 있었습니다.

---

### 12.4 Vivado Block Design Address Map 문제

**🔍 문제 상황**

  * MicroBlaze RISC-V에서 주변장치에 접근할 때 일부 IP가 정상적으로 동작하지 않는 문제가 발생할 수 있었습니다.

**❓ 원인 분석**

  * AXI 기반 주변장치는 각각 고유한 주소 영역을 가져야 합니다.
  * 주소가 겹치거나 Address Editor 설정이 누락되면 소프트웨어에서 해당 장치를 정상적으로 제어하기 어렵습니다.

**❗ 해결 방법**

  * Address Editor에서 AXI GPIO, AXI UARTLite, AXI Timer, AXI Quad SPI의 주소 영역을 각각 분리했습니다.
  * 각 IP의 Base Address를 확인하고, Vitis에서 동일한 주소 정보를 사용하도록 XSA 파일을 생성했습니다.

**✅ 결과**

  * MicroBlaze RISC-V에서 각 주변장치에 안정적으로 접근할 수 있는 구조가 완성되었습니다.
  * Vitis에서 하드웨어 플랫폼을 불러와 소프트웨어 제어를 진행할 수 있게 되었습니다.

---

### 12.5 Reset 신호 극성 문제

**🔍 문제 상황**

  * FPGA에 bitstream을 업로드한 후 시스템이 정상적으로 시작되지 않거나, 리셋 후 주변장치가 동작하지 않는 문제가 발생할 수 있었습니다.

**❓ 원인 분석**

  * Processor System Reset IP와 외부 reset 버튼의 극성이 맞지 않으면 MicroBlaze와 AXI 주변장치가 정상적으로 초기화되지 않습니다.
  * reset 신호는 Clock Wizard와 Processor System Reset에 모두 연결되어 있어 전체 시스템 동작에 영향을 줍니다.

**❗ 해결 방법**

  * Vivado Block Design에서 reset 신호를 Processor System Reset과 Clock Wizard에 연결했습니다.
  * XDC 파일에서 reset 입력 핀을 Basys3 버튼에 맞게 설정했습니다.

**✅ 결과**

  * 리셋 입력 후 MicroBlaze와 AXI 주변장치가 안정적으로 초기화되었습니다.
  * 시스템 시작 과정의 불안정한 동작을 줄일 수 있었습니다.

---

## 🚀 13. Future Improvements (개선 사항)

  * RFID 카드 UID를 사용자 정보와 매칭하여 실제 학생별 좌석 이용 관리 기능 추가
  * 좌석별 이용 시간을 저장하고, 장시간 미사용 좌석을 자동 반납 처리하는 기능 추가
  * LCD에 남은 좌석 수, 현재 좌석 번호, 이용 시간 등을 순차적으로 표시
  * UART를 이용해 PC 프로그램과 연동하고, 좌석 현황을 실시간으로 확인
  * Wi-Fi 또는 Bluetooth 모듈을 추가하여 모바일 화면에서 좌석 상태 확인
  * 여러 개의 좌석을 배열 형태로 관리하여 실제 도서관 좌석 배치도처럼 확장
  * 관리자 모드를 추가하여 전체 좌석 초기화, 강제 반납, 사용 기록 확인 기능 추가

---

## 🧾 14. Result (결과)

본 프로젝트는 Basys3 FPGA 보드에서 MicroBlaze RISC-V 기반의 도서관 좌석 관리 시스템을 구현하기 위한 하드웨어 플랫폼을 구성했습니다.

Vivado Block Design을 이용해 MicroBlaze RISC-V, AXI GPIO, AXI UARTLite, AXI Timer, AXI Quad SPI를 연결했으며, LCD 출력과 SPI 외부 모듈 통신, UART 디버깅이 가능한 구조를 완성했습니다.

이를 통해 FPGA 기반 임베디드 시스템 설계, AXI 버스 기반 주변장치 연결, XDC 핀 제약 설정, Vitis 연동용 XSA 생성 흐름을 실습할 수 있었습니다.
