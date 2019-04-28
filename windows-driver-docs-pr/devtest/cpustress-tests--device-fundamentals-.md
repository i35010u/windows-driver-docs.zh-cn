---
title: CPU 压力测试（设备基础功能）
description: CpuStress 测试执行设备 I/O 测试使用不同的处理器利用率级别。
ms.assetid: E546C3A3-89E6-450B-90D3-4F349A3EC495
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5522ecb85b757e545c62c0b76b84da23104d1d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343053"
---
# <a name="cpustress-tests-device-fundamentals"></a>CPU 压力测试（设备基础功能）


CpuStress 测试执行设备 I/O 测试使用不同的处理器利用率级别。

## <a name="span-idcpustresstestsspanspan-idcpustresstestsspancpustress"></a><span id="cpu_stress_tests"></span><span id="CPU_STRESS_TESTS"></span>CpuStress


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
<td align="left"><p><span id="Device_I_O_with_alternating_processor_utilization_levels"></span><span id="device_i_o_with_alternating_processor_utilization_levels"></span><span id="DEVICE_I_O_WITH_ALTERNATING_PROCESSOR_UTILIZATION_LEVELS"></span>设备 I/O 使用替代的处理器利用率级别</p></td>
<td align="left"><p>此测试执行设备 I/O 测试时高 (HPU) 和低 (LPU) 处理器利用率级别之间交替。</p>
<p><strong>测试二进制文件：</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>测试方法：</strong>Device_IO_With_Varying_ProcUtil</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>PingPongPeriod</em></p>
<p><em>HPU</em></p>
<p><em>LPU</em></p>
<p><em>TestCycles</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Device_I_O_with_a_fixed_processor_utilization_level"></span><span id="device_i_o_with_a_fixed_processor_utilization_level"></span><span id="DEVICE_I_O_WITH_A_FIXED_PROCESSOR_UTILIZATION_LEVEL"></span>设备 I/O 具有固定的处理器利用率级别</p></td>
<td align="left"><p>此测试执行设备 I/O 测试与设置为固定百分比处理器利用率 (PU) 级别。</p>
<p><strong>测试二进制文件：</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>测试方法：</strong>Device_IO_With_Fixed_ProcUtil</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p>
<p><em>PU</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Device_PNP_with_a_fixed_processor_utilization_level"></span><span id="device_pnp_with_a_fixed_processor_utilization_level"></span><span id="DEVICE_PNP_WITH_A_FIXED_PROCESSOR_UTILIZATION_LEVEL"></span>使用固定的处理器利用率级别 PNP 设备</p></td>
<td align="left"><p>此测试执行设备即插即用测试与设置为固定百分比处理器利用率 (PU) 级别。</p>
<p><strong>测试二进制文件：</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>测试方法：</strong>Device_PNP_With_Fixed_ProcUtil</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>PU</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Sleep_with_fixed_processor_utilization_"></span><span id="sleep_with_fixed_processor_utilization_"></span><span id="SLEEP_WITH_FIXED_PROCESSOR_UTILIZATION_"></span>使用固定的处理器使用率进入睡眠状态</p></td>
<td align="left"><p>此测试周期设置为固定百分比处理器利用率级别与通过各种睡眠状态系统。</p>
<p><strong>测试二进制文件：</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>测试方法：</strong>Sleep_With_Fixed_ProcUtil</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>TestCycles</em></p>
<p><em>PU</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/library/windows/hardware/hh781398)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 






