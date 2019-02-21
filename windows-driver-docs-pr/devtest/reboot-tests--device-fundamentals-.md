---
title: 重新启动测试（设备基础功能）
description: 重新启动设备基础测试之前和之后，或在系统重新启动期间，指定设备上运行 I/O。
ms.assetid: 71EBEC60-C99F-412D-8FC5-2DD9209CC92D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3289abffa3cffd28d334971db5257321ece358af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526257"
---
# <a name="reboot-tests-device-fundamentals"></a>重新启动测试（设备基础功能）


重新启动设备基础测试之前和之后，或在系统重新启动期间，指定设备上运行 I/O。

## <a name="span-idreboottestsspanspan-idreboottestsspanreboot-tests"></a><span id="reboot_tests"></span><span id="REBOOT_TESTS"></span>重新启动测试


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
<td align="left"><p><span id="Critical_Reboot_Restart_with_I_O_before_and_after"></span><span id="critical_reboot_restart_with_i_o_before_and_after"></span><span id="CRITICAL_REBOOT_RESTART_WITH_I_O_BEFORE_AND_AFTER"></span>关键的重启为重新启动 I/O 之前和之后</p></td>
<td align="left"><p>之前和之后的关键系统重启，在该测试在设备上运行 I/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_Critical_RebootRestart_With_IO_BeforeAndAfter.wsc</p>
<p><strong>测试方法：</strong>Critical_Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Critical_Reboot_Restart_with_I_O_during"></span><span id="critical_reboot_restart_with_i_o_during"></span><span id="CRITICAL_REBOOT_RESTART_WITH_I_O_DURING"></span>使用期间的 I/O 的关键的重新启动重新启动</p></td>
<td align="left"><p>此测试在设备上启动简单的 I/O、 启动 I/O 运行时，关键的重新启动并在重新启动后再次运行 SimpleI/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_Critical_RebootRestart_With_IO_During.wsc</p>
<p><strong>测试方法：</strong>Critical_Reboot_Restart_With_IO_During</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Reboot_Restart_with_I_O_before_and_after"></span><span id="reboot_restart_with_i_o_before_and_after"></span><span id="REBOOT_RESTART_WITH_I_O_BEFORE_AND_AFTER"></span>重新启动为重新启动 I/O 之前和之后</p></td>
<td align="left"><p>之前和之后的系统重启，在该测试在设备上运行 I/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_RebootRestart_With_IO_BeforeAndAfter.wsc</p>
<p><strong>测试方法：</strong>Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Reboot_restart_with_I_O_during"></span><span id="reboot_restart_with_i_o_during"></span><span id="REBOOT_RESTART_WITH_I_O_DURING"></span>重新启动期间的 I/O 为重新启动</p></td>
<td align="left"><p>此测试在设备上启动简单的 I/O、 启动 I/O 运行时，重新启动并在重新启动后再次运行 SimpleI/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_RebootRestart_With_IO_During.wsc</p>
<p><strong>测试方法：</strong>Reboot_Restart_With_IO_During</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[设备基础测试](device-fundamentals-tests.md)

[设备基础测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[提供 WDTF 简单 I/O 插件](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[如何测试在运行时从命令提示符下的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 






