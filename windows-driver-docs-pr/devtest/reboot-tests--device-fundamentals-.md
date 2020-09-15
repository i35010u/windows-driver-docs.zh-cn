---
title: 重新启动测试（设备基础功能）
description: 设备基础重新启动测试在指定的设备上、之前和之后或在系统重启期间运行 i/o。
ms.assetid: 71EBEC60-C99F-412D-8FC5-2DD9209CC92D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57a6c4f7e7207d3fd3722644ef788a04859d1786
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107508"
---
# <a name="reboot-tests-device-fundamentals"></a>重新启动测试（设备基础功能）


设备基础重新启动测试在指定的设备上、之前和之后或在系统重启期间运行 i/o。

## <a name="span-idreboot_testsspanspan-idreboot_testsspanreboot-tests"></a><span id="reboot_tests"></span><span id="REBOOT_TESTS"></span>重新启动测试


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
<td align="left"><p><span id="Critical_Reboot_Restart_with_I_O_before_and_after"></span><span id="critical_reboot_restart_with_i_o_before_and_after"></span><span id="CRITICAL_REBOOT_RESTART_WITH_I_O_BEFORE_AND_AFTER"></span>关键重启在前后 i/o</p></td>
<td align="left"><p>此测试在关键系统重启前后在设备上运行 i/o。</p>
<p><strong>测试二进制文件：</strong> Devfund_Critical_RebootRestart_With_IO_BeforeAndAfter. wsc</p>
<p><strong>测试方法：</strong> Critical_Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Critical_Reboot_Restart_with_I_O_during"></span><span id="critical_reboot_restart_with_i_o_during"></span><span id="CRITICAL_REBOOT_RESTART_WITH_I_O_DURING"></span>在期间的 i/o 重新启动关键</p></td>
<td align="left"><p>此测试启动设备上的简单 i/o，启动运行 i/o 的关键重启，并在重新启动后再次运行 SimpleI/O。</p>
<p><strong>测试二进制文件：</strong> Devfund_Critical_RebootRestart_With_IO_During. wsc</p>
<p><strong>测试方法：</strong> Critical_Reboot_Restart_With_IO_During</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Reboot_Restart_with_I_O_before_and_after"></span><span id="reboot_restart_with_i_o_before_and_after"></span><span id="REBOOT_RESTART_WITH_I_O_BEFORE_AND_AFTER"></span>重新启动，并在前后 i/o</p></td>
<td align="left"><p>此测试在系统重启前后在设备上运行 i/o。</p>
<p><strong>测试二进制文件：</strong> Devfund_RebootRestart_With_IO_BeforeAndAfter. wsc</p>
<p><strong>测试方法：</strong> Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Reboot_restart_with_I_O_during"></span><span id="reboot_restart_with_i_o_during"></span><span id="REBOOT_RESTART_WITH_I_O_DURING"></span>在过程中，通过 i/o 重新启动</p></td>
<td align="left"><p>此测试启动设备上的简单 i/o，启动运行 i/o 的重新启动，并在重新启动后再次运行 SimpleI/O。</p>
<p><strong>测试二进制文件：</strong> Devfund_RebootRestart_With_IO_During. wsc</p>
<p><strong>测试方法：</strong> Reboot_Restart_With_IO_During</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
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

