---
title: IoSpy
description: IoSpy 是记录有关对设备的内核模式驱动程序的 IOCTL 和 WMI 请求数据的筛选器驱动程序。
ms.assetid: 5fe52fe6-97b4-477a-9450-727c5bf9bd72
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: f3ccbd84b0f29683d6d94495fd8563d214be76a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519473"
---
> [!NOTE]
> IoSpy 和 IoAttack 不再在 WDK 中可用后 Windows 10 版本 1703年。
>
> 作为这些工具的替代方法，请考虑使用 HLK 中可用的模糊测试。 下面是一些需要考虑。
> 
> [DF-模糊随机 IOCTL 测试 （可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)
>
> [DF-模糊子打开测试 （可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)
>
> [DF-模糊零长度的缓冲区 FSCTL 测试 （可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)
>
> [DF-模糊随机 FSCTL 测试 （可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)
>
> [DF-模糊杂项 API 测试 （可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)
>
> 此外可以使用[内核同步延迟模糊](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)随驱动程序验证程序。
>



# <a name="iospy"></a>IoSpy


IoSpy 是记录有关对设备的内核模式驱动程序的 IOCTL 和 WMI 请求数据的筛选器驱动程序。

可以安装和删除使用 IoSpy [（设备基础） 的渗透测试](coverage-tests--device-fundamentals-.md)测试，**启用 I/O Spy**并**禁用 I/O Spy**。 *DQ*参数控制哪些设备安装 IoSpy 筛选器驱动程序。 IoSpy 记录中的 IOCTL 和 WMI 请求有关的详细信息[IoSpy 数据文件](#iospy-data-file)，以供[IoAttack](ioattack.md)执行模糊测试。

**重要**  运行 IoAttack 之前，必须之前已运行 IoSpy 的虚拟机和模板，然后从测试系统中删除它。 有关详细信息，请参阅[如何使用 IoSpy 和 IoAttack 执行模糊测试](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Disable_I_O_Spy"></span><span id="disable_i_o_spy"></span><span id="DISABLE_I_O_SPY"></span>禁用 I/O Spy</p></td>
<td align="left"><p>一个或多个设备上禁用 I/O Spy。 卸载 IoSpy 并禁用 IOCTL 和 WMI 筛选的测试系统上的所有设备。</p>
<p><strong>测试二进制文件：</strong>Devfund_IOSpy_DisableSupport.wsc</p>
<p><strong>测试方法：</strong>DisableIoSpy</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_I_O_Spy-enabled_Device"></span><span id="display_i_o_spy-enabled_device"></span><span id="DISPLAY_I_O_SPY-ENABLED_DEVICE"></span>显示 I/O Spy 启用设备</p></td>
<td align="left"><p>显示具有 I/O Spy 启用的设备。</p>
<p><strong>测试二进制文件：</strong>Devfund_IOSpy_DisplayEnabledDevices.wsc</p>
<p><strong>测试方法：</strong>DisplayIoSpyDevices</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_I_O_Spy_"></span><span id="enable_i_o_spy_"></span><span id="ENABLE_I_O_SPY_"></span>启用 I/O Spy</p></td>
<td align="left"><p>测试系统上安装 IoSpy 并启用 IOCTL 和 WMI 筛选一个或多个设备上。 DQ 参数控制 IoSpy 筛选器驱动程序将安装在哪些设备。</p>
<p><strong>测试二进制文件：</strong>Devfund_IOSpy_EnableSupport.wsc</p>
<p><strong>测试方法：</strong>EnableIoSpy</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>DFD</em> -指定 IoSpy 数据文件的路径。 默认位置是 %SystemDrive%\DriverTest\IoSpy</p></td>
</tr>
</tbody>
</table>

 

## <a name="iospy-data-file"></a>IoSpy 数据文件

IoSpy 安装测试系统中后，它会记录通过 IOCTL 和 WMI 请求发送到驱动程序，为设备启用的模糊测试的数据。 虽然 IoSpy 不会分析这些请求的负载，它记录的详细信息，如负载缓冲区的长度的请求。

*DFD*参数**启用 I/O Spy**测试指定 IoSpy 数据文件的路径。 默认位置是 %systemdrive%\\DriverTest\\IoSpy

 

 





