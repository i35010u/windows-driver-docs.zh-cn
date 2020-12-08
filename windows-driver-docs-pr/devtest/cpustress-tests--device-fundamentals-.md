---
title: CPU 压力测试（设备基础功能）
description: CpuStress 测试将执行具有不同处理器利用率级别的设备 i/o 测试。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d088cbdbfd8c5ddba1e48f9918cea71a6b9f2880
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801837"
---
# <a name="cpustress-tests-device-fundamentals"></a>CPU 压力测试（设备基础功能）


CpuStress 测试将执行具有不同处理器利用率级别的设备 i/o 测试。

## <a name="span-idcpu_stress_testsspanspan-idcpu_stress_testsspancpustress"></a><span id="cpu_stress_tests"></span><span id="CPU_STRESS_TESTS"></span>CpuStress


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
<td align="left"><p><span id="Device_I_O_with_alternating_processor_utilization_levels"></span><span id="device_i_o_with_alternating_processor_utilization_levels"></span><span id="DEVICE_I_O_WITH_ALTERNATING_PROCESSOR_UTILIZATION_LEVELS"></span>处理器利用率级别交替的设备 i/o</p></td>
<td align="left"><p>此测试执行设备 i/o 测试，同时交替使用高 (HPU) 和低 (LPU) 处理器利用率级别。</p>
<p><strong>测试二进制文件：</strong> Devfund_ProcUtil_PingPong_With_IO. wsc</p>
<p><strong>测试方法：</strong> Device_IO_With_Varying_ProcUtil</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>PingPongPeriod</em></p>
<p><em>HPU</em></p>
<p><em>LPU</em></p>
<p><em>TestCycles</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Device_I_O_with_a_fixed_processor_utilization_level"></span><span id="device_i_o_with_a_fixed_processor_utilization_level"></span><span id="DEVICE_I_O_WITH_A_FIXED_PROCESSOR_UTILIZATION_LEVEL"></span>具有固定处理器利用率级别的设备 i/o</p></td>
<td align="left"><p>此测试执行的是处理器使用率 (PU) 级别设置为固定百分比的设备 i/o 测试。</p>
<p><strong>测试二进制文件：</strong> Devfund_ProcUtil_PingPong_With_IO. wsc</p>
<p><strong>测试方法：</strong> Device_IO_With_Fixed_ProcUtil</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p>
<p><em>PU</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Device_PNP_with_a_fixed_processor_utilization_level"></span><span id="device_pnp_with_a_fixed_processor_utilization_level"></span><span id="DEVICE_PNP_WITH_A_FIXED_PROCESSOR_UTILIZATION_LEVEL"></span>具有固定处理器利用率级别的设备 PNP</p></td>
<td align="left"><p>此测试通过处理器使用率进行设备 PNP 测试， (PU) 级别设置为固定百分比。</p>
<p><strong>测试二进制文件：</strong> Devfund_ProcUtil_PingPong_With_IO. wsc</p>
<p><strong>测试方法：</strong> Device_PNP_With_Fixed_ProcUtil</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>PU</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Sleep_with_fixed_processor_utilization_"></span><span id="sleep_with_fixed_processor_utilization_"></span><span id="SLEEP_WITH_FIXED_PROCESSOR_UTILIZATION_"></span>固定处理器利用率的睡眠</p></td>
<td align="left"><p>此测试通过各种睡眠状态将系统循环，处理器使用率级别设置为固定百分比。</p>
<p><strong>测试二进制文件：</strong> Devfund_ProcUtil_PingPong_With_IO. wsc</p>
<p><strong>测试方法：</strong> Sleep_With_Fixed_ProcUtil</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>TestCycles</em></p>
<p><em>PU</em></p></td>
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

