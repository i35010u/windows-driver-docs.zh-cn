---
title: I/O 测试（设备基础功能）
description: 设备基础 I/O 测试执行基本的 I/O 测试，在指定的设备上。
ms.assetid: 4FF125BE-846A-4A93-9B4F-C6BC469EA0AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eb8dd3ef53d503193938b8cc0e66d6e416a10d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356512"
---
# <a name="io-tests-device-fundamentals"></a>I/O 测试（设备基础功能）


设备基础 I/O 测试执行基本的 I/O 测试，在指定的设备上。

## <a name="span-idiotestsspanspan-idiotestsspanio-tests"></a><span id="io_tests"></span><span id="IO_TESTS"></span>I/O 测试中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">测试</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Device_I_O_"></span><span id="device_i_o_"></span><span id="DEVICE_I_O_"></span>设备 I/O</p></td>
<td align="left"><p>此测试可执行基本的 I/O 测试，在设备上。</p>
<p><strong>测试二进制文件：</strong>Devfund_Device_IO.wsc</p>
<p><strong>测试方法：</strong>DeviceIO</p>
<p><strong>参数：</strong> -请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>IOPeriod</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Simple_I_O_stress_test_with_I_O_process_termination"></span><span id="simple_i_o_stress_test_with_i_o_process_termination"></span><span id="SIMPLE_I_O_STRESS_TEST_WITH_I_O_PROCESS_TERMINATION"></span>与 I/O 进程终止的简单 I/O 压力测试</p></td>
<td align="left"><p>此测试执行简单的单独进程中的设备上的 I/O 测试并在指定的 I/O 周期和测试周期后终止 I/O 进程。</p>
<p><strong>测试二进制文件：</strong>Devfund_SimpleIoStress_TermIoProc.wsc</p>
<p><strong>测试方法：</strong>SimpleIOStress_TermIoProc</p>
<p><strong>参数：</strong> -请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](https://docs.microsoft.com/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

 

 






