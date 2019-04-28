---
title: 混沌测试（设备基础功能）
description: （并发硬件和操作系统） 的混沌测试运行各种即插即用驱动程序测试、 设备驱动程序模糊测试，并关闭系统同时测试。
ms.assetid: FA0D73DC-B0B8-4CA7-8DDC-A2C3EC106C3F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ba7b831802cf9ffe7b76bc5b29526a0c10cbf23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343981"
---
# <a name="chaos-tests-device-fundamentals"></a>混沌测试（设备基础功能）


（并发硬件和操作系统） 的混沌测试运行各种即插即用驱动程序测试、 设备驱动程序模糊测试，并关闭系统同时测试。

### <a name="span-idcoveragetestsspanspan-idcoveragetestsspanchaos-tests"></a><span id="coverage_tests"></span><span id="COVERAGE_TESTS"></span>混沌测试

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
<td align="left"><p><span id="Disable_Enhanced_Device_Testing__EDT__Support_"></span><span id="disable_enhanced_device_testing__edt__support_"></span><span id="DISABLE_ENHANCED_DEVICE_TESTING__EDT__SUPPORT_"></span>禁用增强的设备测试 (EDT) 支持</p></td>
<td align="left"><p>此测试卸载测试筛选器驱动程序 (msdmfilt.sys) 作为使用 DQ 参数指定的设备上的上限筛选器。 此测试筛选器获取作为此测试类别运行测试的一部分安装</p>
<p>即插即用驱动程序测试使用 EDT 筛选器驱动程序将 IRP_MN_CANCEL_REMOVE_DEVICE 发送到目标设备堆栈。</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Run_CHAOS_Test"></span><span id="run_chaos_test"></span><span id="RUN_CHAOS_TEST"></span>运行混沌测试</p></td>
<td align="left"><p>运行 PnP 测试和模糊测试并行循环访问所有受支持的系统电源状态通过系统。 即插即用驱动程序测试执行即插即用的操作时将 I/O 请求发送到目标设备堆栈。</p>
<p>此测试运行即插即用测试 （禁用/启用、 重新平衡、 删除/重新启动、 意外删除和 DIF 删除） 和驱动程序模糊测试并行情况下，在测试设备时循环入和移出所有受支持的休眠状态 （S1、 S2、 S3、 S4 和已连接的测试系统备用） 在同一时间。 此测试的目的是测试 PNP、 I/O 和 Power 并发方案，并查找任何崩溃和/或在过程中挂起。</p>
<p><strong>测试二进制文件：</strong>Devfund_ChaosTest.dll</p>
<p><strong>测试方法：</strong>RunCHAOSTest</p>
<p><strong>参数：</strong></p>
<p><em>DQ</em> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>TestPeriod</em> -指定多长时间运行的测试 （以分钟为单位）。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[PwrTest](pwrtest.md)

[渗透压力测试（设备基础功能）](penetration-tests--device-fundamentals-.md)

[即插即用测试 （设备基础知识）](pnp-tests--device-fundamentals-.md)

 

 






