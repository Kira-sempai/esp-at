硬件连接
========

:link_to_translation:`en:[English]`

本文档主要介绍下载和烧录 AT 固件、发送 AT 命令和接收 AT 响应所需要的硬件以及硬件之间该如何连接。

对于不同系列的模组，AT 默认固件所支持的命令会有所差异。具体可参考 :doc:`/Compile_and_Develop/esp-at_firmware_differences`。

硬件准备
------------

.. list-table:: ESP-AT 测试所需硬件
   :header-rows: 1

   * - 硬件
     - 功能
   * - {IDF_TARGET_NAME} 开发板
     - 从机
   * - USB 数据线（连接 {IDF_TARGET_NAME} 开发板和 PC）
     - 下载固件、输出日志数据连接
   * - PC
     - 主机，将固件下载至从机
   * - USB 数据线（连接 PC 和 USB 转 UART 串口模块）
     - 发送 AT 命令、接收 AT 响应数据连接
   * - USB 转 UART 串口模块
     - 转换 USB 信号和 TTL 信号
   * - 杜邦线（连接 USB 转 UART 串口模块和 {IDF_TARGET_NAME} 开发板）
     - 发送 AT 命令、接收 AT 响应数据连接

.. figure:: ../../_static/hw-connection-what-you-need.png
   :align: center
   :alt: ESP-AT 测试硬件连接示意图
   :figclass: align-center

   ESP-AT 测试硬件连接示意图

注意：上图使用 4 根杜邦线连接 {IDF_TARGET_NAME} 开发板和 USB 转 UART 串口模块，但如果您不使用硬件流控功能，只需 2 根杜邦线连接 TX/RX 即可。

.. only:: esp32

  {IDF_TARGET_NAME} 系列
  -----------------------

  {IDF_TARGET_NAME} AT 采用两个 UART 接口：UART0 用于下载固件和输出日志，UART1 用于发送 AT 命令和接收 AT 响应。默认情况下，UART0 和 UART1 均使用 ``115200`` 波特率进行通信。

  所有 {IDF_TARGET_NAME} 模组均连接 GPIO1 和 GPIO3 作为 UART0，但连接不同的 GPIO 作为 UART1，下文将详细介绍如何连接 {IDF_TARGET_NAME} 系列模组。

  更多有关 {IDF_TARGET_NAME} 模组和开发板的信息可参考 `{IDF_TARGET_NAME} 系列模组和开发板 <https://docs.espressif.com/projects/esp-idf/zh_CN/stable/hw-reference/modules-and-boards.html>`_。

  ESP32-WROOM-32 系列
  ^^^^^^^^^^^^^^^^^^^^^^

  .. list-table:: ESP32-WROOM-32 系列硬件连接管脚分配
    :header-rows: 1

    * - 功能
      - {IDF_TARGET_NAME} 开发板管脚
      - 其它设备管脚
    * - 下载固件/输出日志 :sup:`1`
      - UART0
          * GPIO3 (RX)
          * GPIO1 (TX)
      - PC
          * TX
          * RX
    * - AT 命令/响应 :sup:`2`
      - UART1
          * GPIO16 (RX)
          * GPIO17 (TX)
          * GPIO15 (CTS)
          * GPIO14 (RTS)
      - USB 转 UART 串口模块
          * TX
          * RX
          * RTS
          * CTS

  **说明** 1：{IDF_TARGET_NAME} 开发板和 PC 之间的管脚连接已内置在 {IDF_TARGET_NAME} 开发板上，您只需使用 USB 数据线连接开发板和 PC 即可。

  **说明** 2：CTS/RTS 管脚只有在使用硬件流控功能时才需连接。

  .. figure:: ../../_static/esp32-wroom-hw-connection.png
    :align: center
    :alt: ESP32-WROOM-32 系列硬件连接示意图
    :figclass: align-center

    ESP32-WROOM-32 系列硬件连接示意图

  如果需要直接基于 ESP32-WROOM-32 模组进行连接，请参考 `《ESP32-WROOM-32 技术规格书》 <https://www.espressif.com/sites/default/files/documentation/esp32_wrover_datasheet_cn.pdf>`_。

  .. _hw-connection-esp32-wrover-series:

  ESP32-WROVER 系列
  ^^^^^^^^^^^^^^^^^^^^^^^^
  .. list-table:: ESP32-WROVER 系列硬件连接管脚分配
    :header-rows: 1

    * - 功能
      - {IDF_TARGET_NAME} 开发板管脚
      - 其它设备管脚
    * - 下载固件/输出日志 :sup:`1`
      - UART0
          * GPIO3 (RX)
          * GPIO1 (TX)
      - PC
          * TX
          * RX
    * - AT 命令/响应 :sup:`2`
      - UART1
          * GPIO19 (RX)
          * GPIO22 (TX)
          * GPIO15 (CTS)
          * GPIO14 (RTS)
      - USB 转 UART 串口模块
          * TX
          * RX
          * RTS
          * CTS

  **说明** 1：{IDF_TARGET_NAME} 开发板和 PC 之间的管脚连接已内置在 {IDF_TARGET_NAME} 开发板上，您只需使用 USB 数据线连接开发板和 PC 即可。

  **说明** 2：CTS/RTS 管脚只有在使用硬件流控功能时才需连接。

  .. figure:: ../../_static/esp32-wrover-hw-connection.png
    :align: center
    :alt: ESP32-WROVER 系列硬件连接示意图
    :figclass: align-center

    ESP32-WROVER 系列硬件连接示意图

  如果需要直接基于 ESP32-WROVER 模组进行连接，请参考 `《ESP32-WROVER 技术规格书》 <https://www.espressif.com/sites/default/files/documentation/esp32_wrover_datasheet_cn.pdf>`_。

  ESP32-PICO 系列
  ^^^^^^^^^^^^^^^^^^

  .. list-table:: ESP32-PICO 系列硬件连接管脚分配
    :header-rows: 1

    * - 功能
      - {IDF_TARGET_NAME} 开发板管脚
      - 其它设备管脚
    * - 下载固件/输出日志 :sup:`1`
      - UART0
          * GPIO3 (RX)
          * GPIO1 (TX)
      - PC
          * TX
          * RX
    * - AT 命令/响应 :sup:`2`
      - UART1
          * GPIO19 (RX)
          * GPIO22 (TX)
          * GPIO15 (CTS)
          * GPIO14 (RTS)
      - USB 转 UART 串口模块
          * TX
          * RX
          * RTS
          * CTS

  **说明** 1：{IDF_TARGET_NAME} 开发板和 PC 之间的管脚连接已内置在 {IDF_TARGET_NAME} 开发板上，您只需使用 USB 数据线连接开发板和 PC 即可。

  **说明** 2：CTS/RTS 管脚只有在使用硬件流控功能时才需连接。

  .. figure:: ../../_static/esp32-pico-hw-connection.png
    :align: center
    :alt: ESP32-PICO 系列硬件连接示意图
    :figclass: align-center

    ESP32-PICO 系列硬件连接示意图

  如果需要直接基于 ESP32-PICO-D4 进行连接，请参考 `《ESP32-PICO-D4 技术规格书》 <https://www.espressif.com/sites/default/files/documentation/esp32-pico-d4_datasheet_cn.pdf>`_。

  ESP32-SOLO 系列
  ^^^^^^^^^^^^^^^^^^

  .. list-table:: ESP32-SOLO 系列硬件连接管脚分配
    :header-rows: 1

    * - 功能
      - {IDF_TARGET_NAME} 开发板管脚
      - 其它设备管脚
    * - 下载固件/输出日志 :sup:`1`
      - UART0
          * GPIO3 (RX)
          * GPIO1 (TX)
      - PC
          * TX
          * RX
    * - AT 命令/响应 :sup:`2`
      - UART1
          * GPIO16 (RX)
          * GPIO17 (TX)
          * GPIO15 (CTS)
          * GPIO14 (RTS)
      - USB 转 UART 串口模块
          * TX
          * RX
          * RTS
          * CTS

  **说明** 1：{IDF_TARGET_NAME} 开发板和 PC 之间的管脚连接已内置在 {IDF_TARGET_NAME} 开发板上，您只需使用 USB 数据线连接开发板和 PC 即可。

  **说明** 2：CTS/RTS 管脚只有在使用硬件流控功能时才需连接。

  .. figure:: ../../_static/esp32-solo-hw-connection.png
    :align: center
    :alt: ESP32-SOLO 系列硬件连接示意图
    :figclass: align-center

    ESP32-SOLO 系列硬件连接示意图

  如果需要直接基于 ESP32-SOLO-1 进行连接，请参考 `《ESP32-SOLO-1 技术规格书》 <https://www.espressif.com/sites/default/files/documentation/esp32-solo-1_datasheet_cn.pdf>`_。

.. only:: esp32c2

  {IDF_TARGET_NAME} 系列
  -----------------------

  {IDF_TARGET_NAME} AT 采用两个 UART 接口：UART0 用于下载固件和输出日志，UART1 用于发送 AT 命令和接收 AT 响应。默认情况下，UART0 和 UART1 均使用 ``115200`` 波特率进行通信。

  .. list-table:: {IDF_TARGET_NAME} Series 系列硬件连接管脚分配
    :header-rows: 1

    * - 功能
      - {IDF_TARGET_NAME} 开发板管脚
      - 其它设备管脚
    * - 下载固件/输出日志 :sup:`1`
      - UART0
          * GPIO20 (RX)
          * GPIO21 (TX)
      - PC
          * TX
          * RX
    * - AT 命令/响应 :sup:`2`
      - UART1
          * GPIO6 (RX)
          * GPIO7 (TX)
          * GPIO5 (CTS)
          * GPIO4 (RTS)
      - USB 转 UART 串口模块
          * TX
          * RX
          * RTS
          * CTS

  **说明** 1：{IDF_TARGET_NAME} 开发板和 PC 之间的管脚连接已内置在 {IDF_TARGET_NAME} 开发板上，您只需使用 USB 数据线连接开发板和 PC 即可。

  **说明** 2：CTS/RTS 管脚只有在使用硬件流控功能时才需连接。

  .. figure:: ../../_static/esp32-c2-hw-connection.png
    :align: center
    :alt: {IDF_TARGET_NAME} 系列硬件连接示意图
    :figclass: align-center

    {IDF_TARGET_NAME} 系列硬件连接示意图

  如果需要直接基于 ESP32-C2-MINI-1 模组进行连接，请参考 `《ESP32-C2-MINI-1 技术规格书》 <https://www.espressif.com/sites/default/files/documentation/esp32-c2-mini-1_datasheet_cn.pdf>`_。

.. only:: esp32c3

  {IDF_TARGET_NAME} 系列
  -----------------------

  {IDF_TARGET_NAME} AT 采用两个 UART 接口：UART0 用于下载固件和输出日志，UART1 用于发送 AT 命令和接收 AT 响应。默认情况下，UART0 和 UART1 均使用 ``115200`` 波特率进行通信。

  .. list-table:: {IDF_TARGET_NAME} Series 系列硬件连接管脚分配
    :header-rows: 1

    * - 功能
      - {IDF_TARGET_NAME} 开发板管脚
      - 其它设备管脚
    * - 下载固件/输出日志 :sup:`1`
      - UART0
          * GPIO20 (RX)
          * GPIO21 (TX)
      - PC
          * TX
          * RX
    * - AT 命令/响应 :sup:`2`
      - UART1
          * GPIO6 (RX)
          * GPIO7 (TX)
          * GPIO5 (CTS)
          * GPIO4 (RTS)
      - USB 转 UART 串口模块
          * TX
          * RX
          * RTS
          * CTS

  **说明** 1：{IDF_TARGET_NAME} 开发板和 PC 之间的管脚连接已内置在 {IDF_TARGET_NAME} 开发板上，您只需使用 USB 数据线连接开发板和 PC 即可。

  **说明** 2：CTS/RTS 管脚只有在使用硬件流控功能时才需连接。

  .. figure:: ../../_static/esp32-c3-hw-connection.png
    :align: center
    :alt: {IDF_TARGET_NAME} 系列硬件连接示意图
    :figclass: align-center

    {IDF_TARGET_NAME} 系列硬件连接示意图

  如果需要直接基于 ESP32-C3-MINI-1 模组进行连接，请参考 `《ESP32-C3-MINI-1 技术规格书》 <https://www.espressif.com/sites/default/files/documentation/esp32-c3-mini-1_datasheet_cn.pdf>`_。
