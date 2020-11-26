---
title: 使用 MITT 购买硬件
description: 若要使用多个接口测试工具 (MITT) ，请按顺序使用 MITT 板，并将特定于总线的适配器插入到 MITT 板上的端口。 适配器的类型取决于要测试的总线。
ms.assetid: 268217FF-0F0B-4175-B2DE-A45FAF94EA79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8a936c61ae0c36a4e10558cfb11fd233cb39d51
ms.sourcegitcommit: 0c3cab853b0b75149b7604eef03275f997792a84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96157279"
---
# <a name="buy-hardware-for-using-mitt"></a>使用 MITT 购买硬件

多接口测试工具 (MITT) 是一项测试工具，用于验证简单外设总线（例如 UART、I2C、SPI 和 GPIO）的硬件和软件。 MITT 使用 FPGA 开发板并提供一个软件包，其中包含固件、测试二进制文件和驱动程序，是一个成本较低的测试解决方案。

若要使用多接口测试工具 (MITT) ，需要一个 MITT 板和特定于总线的适配器，将其插入到 MITT 板上的端口。 适配器的类型取决于要测试的总线。

- **MITT 板**

    例如，FPGA 开发板 (Nexys2) 。 请参阅 [FPGA 板 From Digilent](https://store.digilentinc.com/nexys-2-spartan-3e-fpga-trainer-board-retired-see-nexys-4-ddr/)。

    ![mitt 板](images/g73a5707.jpg)

- **UART/SPI 适配器板**

    请参阅 [JJG 技术中的 UART/SPI 适配器板。](http://www.jjgtechnologies.com/UART-SPI.htm)

    ![uart 适配器板](images/uart1.png)

- **GPIO 适配器板**

    请参阅 [来自 JJG 技术的 GPIO 适配器板。](http://www.jjgtechnologies.com/GPIO.htm)

    ![用于 mitt 的 gpio 适配器](images/gpioadapter.jpg)

- **I2C 适配器板**

    请参阅 [I2C adapter 板 FROM JJG 技术。](http://www.jjgtechnologies.com/I2C.htm)

    ![用于 mitt 的 i2c 适配器](images/i2cadapter.jpg)

- **MCATT 扩展板**

    请参阅 [MCATT 扩展板 FROM JJG 技术。](http://www.jjgtechnologies.com/mcatt.htm)

    ![mcatt 扩展板](images/mcatt-exp.jpg)

- **触摸模拟器 pad**

    触摸模拟器 pad 和带缆线连接到适配器。 MCATT 工具可以通过具激励性与该主板联系的准确点来放大电容式 touch 设备。 可以自定义这些板，使其具有不同的大小和联系点分辨率。

    ![触摸模拟器 pad](images/touch.jpg)

    这些板自定义为设备进行测试。

  - 特定大小
  - 触点数量
  - 触摸点之间的距离

## <a name="related-topics"></a>相关主题

[通过多接口测试工具进行测试 (MITT) ](./testing-with-multi-interface-test-tool--mitt-.md)