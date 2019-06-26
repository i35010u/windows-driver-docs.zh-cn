---
title: 使用多接口测试工具 (MITT) 进行测试
description: MITT 是用于验证的简单外围总线，例如 UART、 I2C、 SPI 和 GPIO 硬件和软件的测试工具。
ms.assetid: B847568F-4872-4FF7-BB73-E45A6FFF8249
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfd1727293c2758635e07a741327164ca76c2c5d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391450"
---
# <a name="test-with-multi-interface-test-tool-mitt"></a>使用多接口测试工具 (MITT) 进行测试


多接口测试工具 (MITT) 是一项测试工具，用于验证简单外设总线（例如 UART、I2C、SPI 和 GPIO）的硬件和软件。 MITT 使用 FPGA 开发板并提供一个软件包，其中包含固件、测试二进制文件和驱动程序，是一个成本较低的测试解决方案。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--" data-raw-source="[Buy hardware for using MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)">购买硬件使用 MITT</a></p></td>
<td><p>为使用多个接口测试工具 (MITT)、 订单需要 MITT 板和总线特定于适配器任务插件板插入 MITT 板上的端口。 适配器看板的类型取决于你想要测试的总线。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---" data-raw-source="[Get started with MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---)">开始使用 MITT</a></p></td>
<td><p>若要运行 MITT 测试，必须在新的 MITT 板上安装 MITT 固件。 以下步骤介绍如何更新 MITT 固件和准备主机计算机上的运行 MITT 测试。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/audio-playback-fidelity-tests-in-mitt" data-raw-source="[Audio playback fidelity tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/audio-playback-fidelity-tests-in-mitt)">MITT 中播放音频保真度测试</a></p></td>
<td><p>MITT 板上的音频模块用于通过检测正弦波频率准确性 （在零叉号），然后计算频率或偏移量不正确的实例来检测在音频设备的传输级别发生的错误。 缺少信号或丢失的数据包会导致移动波形声音且可通过此机制自动检测。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/capacitive-touch-tests-in-mitt" data-raw-source="[Capacitive touch tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/capacitive-touch-tests-in-mitt)">在 MITT 电容式触摸测试</a></p></td>
<td><p>MITT 软件程序包中的电容式触摸测试需要 MCATT （Microsoft 电容式应用程序测试工具）。 它是用于验证基于电容式触控硬件 （触摸板和触摸屏） 自动化工具。 MCATT 包括了用于编程 MCATT 设备和自动的测试的简单接口。 可以使用测试来检测虚影点或确定第一个触摸屏输入传播后系统唤醒时间表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/gpio-tests-in-mitt" data-raw-source="[GPIO tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/gpio-tests-in-mitt)">在 MITT GPIO 测试</a></p></td>
<td><p>MITT 软件程序包中包含的 GPIO 测试模块可用于测试以下按钮卷会关闭电源，以及旋转锁的卷。 可以使用这些测试要检测的 GPIO 驱动程序和微控制器的问题和确定对短期或长期推送的系统响应是否为所需的响应。 附加到按钮的行以物理方式由 MITT 委员会拉取低。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/run-mitt-tests-for-an-i2c-controller-" data-raw-source="[I2C controller tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/run-mitt-tests-for-an-i2c-controller-)">在 MITT I2C 控制器测试</a></p></td>
<td><p>MITT 软件程序包中包含的 I²C 测试模块可用于测试 I²C 控制器和其驱动程序的数据传输。 MITT 板充当客户端设备连接到 I²C 总线。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spi-tests-in-mitt" data-raw-source="[SPI tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/spi-tests-in-mitt)">在 MITT SPI 测试</a></p></td>
<td><p>SPI MITT 软件程序包中包含的测试模块可用于测试 SPI 控制器测试和其驱动程序的系统上的数据传输。 MITT 板充当客户端设备连接到 SPI 总线。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/uart-tests-in-mitt" data-raw-source="[UART tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/uart-tests-in-mitt)">在 MITT UART 测试</a></p></td>
<td><p>MITT 软件程序包包括用于验证数据传输到 UART 控制器和其驱动程序的测试。 MITT 板 UART 接口充当 UART 环回设备。</p></td>
</tr>
</tbody>
</table>

 

 

 




