---
title: I/O 测试（设备基础功能）
description: 设备基础 i/o 测试在指定设备上执行基本 i/o 测试。
ms.assetid: 4FF125BE-846A-4A93-9B4F-C6BC469EA0AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afd348820fce1bd3a8e6a57b664bb68dff1043cd
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107108"
---
# <a name="io-tests-device-fundamentals"></a>I/O 测试（设备基础功能）


设备基础 i/o 测试在指定设备上执行基本 i/o 测试。

## <a name="span-idio_testsspanspan-idio_testsspanio-tests"></a><span id="io_tests"></span><span id="IO_TESTS"></span>I/o 测试


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">测试</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Device_I_O_"></span><span id="device_i_o_"></span><span id="DEVICE_I_O_"></span>设备 i/o</p></td>
<td align="left"><p>此测试在设备上执行基本 i/o 测试。</p>
<p><strong>测试二进制文件：</strong> Devfund_Device_IO. wsc</p>
<p><strong>测试方法：</strong> DeviceIO</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>IOPeriod</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Simple_I_O_stress_test_with_I_O_process_termination"></span><span id="simple_i_o_stress_test_with_i_o_process_termination"></span><span id="SIMPLE_I_O_STRESS_TEST_WITH_I_O_PROCESS_TERMINATION"></span>I/o 处理终止的简单 i/o 压力测试</p></td>
<td align="left"><p>此测试在单独的进程中对设备执行简单的 i/o 测试，并在指定 i/o 周期和测试周期后终止 i/o 进程。</p>
<p><strong>测试二进制文件：</strong> Devfund_SimpleIoStress_TermIoProc. wsc</p>
<p><strong>测试方法：</strong> SimpleIOStress_TermIoProc</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](/windows-hardware/drivers)

[如何选择和配置设备基础功能测试](/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](../wdtf/provided-wdtf-simpleio-plug-ins.md)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](/windows-hardware/drivers)

