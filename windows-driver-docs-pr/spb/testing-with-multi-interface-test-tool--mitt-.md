---
title: 使用多接口测试工具 (MITT) 进行测试
description: MITT 是一种测试工具，用于验证简单外围总线（如 UART、I2C、SPI 和 GPIO）的硬件和软件。
ms.assetid: B847568F-4872-4FF7-BB73-E45A6FFF8249
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d783cec8127139c19b80430457571cd653c9cae4
ms.sourcegitcommit: c766ab74e32eb44795cbbd1a4f352d3a6a9adc14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89389539"
---
# <a name="test-with-multi-interface-test-tool-mitt"></a>使用多接口测试工具 (MITT) 进行测试


多接口测试工具 (MITT) 是一项测试工具，用于验证简单外设总线（例如 UART、I2C、SPI 和 GPIO）的硬件和软件。 MITT 使用 FPGA 开发板并提供一个软件包，其中包含固件、测试二进制文件和驱动程序，是一个成本较低的测试解决方案。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--" data-raw-source="[Buy hardware for using MITT](./multi-interface-test-tool--mitt--.md)">使用 MITT 购买硬件</a></p></td>
<td><p>若要使用多个接口测试工具 (MITT) ，请按顺序使用 MITT 板，并将特定于总线的适配器插入到 MITT 板上的端口。 适配器的类型取决于要测试的总线。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---" data-raw-source="[Get started with MITT](./get-started-with-mitt---.md)">MITT 入门</a></p></td>
<td><p>若要运行 MITT 测试，必须在新的 MITT 板上安装 MITT 固件。 以下步骤介绍了如何更新 MITT 固件并准备好主机以运行 MITT 测试。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/audio-playback-fidelity-tests-in-mitt" data-raw-source="[Audio playback fidelity tests in MITT](./audio-playback-fidelity-tests-in-mitt.md)">MITT 中的音频播放保真度测试</a></p></td>
<td><p>MITT 板上的音频模块用于检测在音频设备传输级别发生的错误，方法是检测正弦波频率准确性 (零交叉) 并统计频率或偏移量不正确的实例。 缺少信号或丢失的数据包将导致移动波形，这种波形可通过此机制自动听到和检测。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/capacitive-touch-tests-in-mitt" data-raw-source="[Capacitive touch tests in MITT](./capacitive-touch-tests-in-mitt.md)">MITT 中的电容式触控测试</a></p></td>
<td><p>MITT 软件包中的电容式触控测试需要 MCATT (Microsoft 电容式应用程序测试工具) 。 它是一个自动化工具，用于验证基于电容式的触摸硬件 (触摸板和 touchscreens) 。 MCATT 包含一个用于对 MCATT 设备进行编程和自动测试的简单接口。 你可以使用这些测试来检测虚影点，或确定第一个触摸输入在系统唤醒后传播的时间表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/gpio-tests-in-mitt" data-raw-source="[GPIO tests in MITT](./gpio-tests-in-mitt.md)">MITT 中的 GPIO 测试</a></p></td>
<td><p>MITT 软件包中包含的 GPIO 测试模块可用于测试以下按钮的音量：向上、向下、向下和旋转锁定。 你可以使用这些测试来检测 GPIO 驱动程序和微控制器的问题，并确定系统是响应短推送还是长推送。 MITT 板以物理方式将附加到按钮的行拉低。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/run-mitt-tests-for-an-i2c-controller-" data-raw-source="[I2C controller tests in MITT](./run-mitt-tests-for-an-i2c-controller-.md)">MITT 中的 I2C 控制器测试</a></p></td>
<td><p>MITT 软件包中包含的 i2c 测试模块可用于测试 i2c 控制器及其驱动程序的数据传输。 MITT 板充当连接到 I i2c 总线的客户端设备。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spi-tests-in-mitt" data-raw-source="[SPI tests in MITT](./spi-tests-in-mitt.md)">MITT 中的 SPI 测试</a></p></td>
<td><p>MITT 软件包中包含的 SPI 测试模块可用于测试数据传输是否适用于受测系统上的 SPI 控制器及其驱动程序。 MITT 板充当连接到 SPI 总线的客户端设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/uart-tests-in-mitt" data-raw-source="[UART tests in MITT](./uart-tests-in-mitt.md)">MITT 中的 UART 测试</a></p></td>
<td><p>MITT 软件包包括用于验证到 UART 控制器及其驱动程序的数据传输的测试。 MITT 板的 UART 接口充当 UART 回送设备。</p></td>
</tr>
</tbody>
</table>

 

 

