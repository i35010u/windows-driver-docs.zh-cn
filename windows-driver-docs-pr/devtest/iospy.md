---
title: IoSpy
description: IoSpy 是一个筛选器驱动程序，用于记录有关 IOCTL 的数据以及对设备的内核模式驱动程序发出的 WMI 请求。
ms.assetid: 5fe52fe6-97b4-477a-9450-727c5bf9bd72
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: ec0134f8d1b51932a9899634a0410116eb68240a
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104610"
---
# <a name="iospy"></a>IoSpy

> [!NOTE]
> Windows 10 1703 版后，WDK 中不再提供 IoSpy 和 IoAttack。
>
> 作为这些工具的替代方法，请考虑使用在 HLK 中提供的模糊化测试。 下面是一些需要考虑的事项。
> 
> [DF - 模糊随机 IOCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)
>
> [DF - 模糊 sub-open 测试（可靠性）](/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)
>
> [DF - 模糊零长度缓冲区 FSCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)
>
> [DF - 模糊随机 FSCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)
>
> [DF - 模糊杂项 API 测试（可靠性）](/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)
>
> 你还可以使用驱动程序验证程序附带的 [内核同步延迟模糊](./kernel-synchronization-delay-fuzzing.md) 处理。
>

IoSpy 是一个筛选器驱动程序，用于记录有关 IOCTL 的数据以及对设备的内核模式驱动程序发出的 WMI 请求。

你可以使用 [渗透测试 (设备基础) ](coverage-tests--device-fundamentals-.md) 测试、 **启用 I/o spy** 和 **禁用 i/o spy**，来安装和删除 IoSpy。 *DQ*参数控制安装 IoSpy 筛选器驱动程序的设备。 IoSpy 记录有关 [IoSpy 数据文件](#iospy-data-file)中的 IOCTL 和 WMI 请求的详细信息， [IoAttack](ioattack.md) 使用此文件执行模糊测试。

**重要提示**   在运行 IoAttack 之前，必须先运行 IoSpy，然后将其从测试系统中删除。 有关详细信息，请参阅 [如何通过 IoSpy 和 IoAttack 执行模糊测试](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Disable_I_O_Spy"></span><span id="disable_i_o_spy"></span><span id="DISABLE_I_O_SPY"></span>禁用 i/o Spy</p></td>
<td align="left"><p>禁用1个或多个设备上的 i/o 监视。 卸载 IoSpy 并为测试系统上的所有设备禁用 IOCTL 和 WMI 筛选。</p>
<p><strong>测试二进制文件：</strong> Devfund_IOSpy_DisableSupport. wsc</p>
<p><strong>测试方法：</strong> DisableIoSpy</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_I_O_Spy-enabled_Device"></span><span id="display_i_o_spy-enabled_device"></span><span id="DISPLAY_I_O_SPY-ENABLED_DEVICE"></span>显示启用了监视的 i/o 设备</p></td>
<td align="left"><p>显示在其上启用了 i/o 监视程序的设备。</p>
<p><strong>测试二进制文件：</strong> Devfund_IOSpy_DisplayEnabledDevices. wsc</p>
<p><strong>测试方法：</strong> DisplayIoSpyDevices</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_I_O_Spy_"></span><span id="enable_i_o_spy_"></span><span id="ENABLE_I_O_SPY_"></span>启用 i/o Spy</p></td>
<td align="left"><p>在测试系统上安装 IoSpy，并在一个或多个设备上启用 IOCTL 和 WMI 筛选。 DQ 参数控制将安装 IoSpy 筛选器驱动程序的设备。</p>
<p><strong>测试二进制文件：</strong> Devfund_IOSpy_EnableSupport. wsc</p>
<p><strong>测试方法：</strong> EnableIoSpy</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>DFD</em> - 指定 IoSpy 数据文件的路径。 默认位置为%SystemDrive%\DriverTest\IoSpy</p></td>
</tr>
</tbody>
</table>

 

## <a name="iospy-data-file"></a>IoSpy 数据文件

在测试系统中安装 IoSpy 后，它将通过 IOCTL 和 WMI 请求发送的数据记录到为模糊测试启用的设备驱动程序的驱动程序中。 尽管 IoSpy 不分析这些请求的负载，但它确实记录了请求的详细信息，例如负载缓冲区的长度。

**启用 I/o 监视**测试的*DFD*参数指定 IoSpy 数据文件的路径。 默认位置为% SystemDrive% \\ DriverTest \\ IoSpy

