---
title: CHAOS 测试（设备基础功能）
description: " (并发硬件和操作系统的混乱) 测试会同时运行各种 PnP 驱动程序测试、设备驱动程序模糊测试和电源系统测试。"
ms.assetid: FA0D73DC-B0B8-4CA7-8DDC-A2C3EC106C3F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f316f52efee5b55b14bb329668f54e5da784b89d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104612"
---
# <a name="chaos-tests-device-fundamentals"></a>CHAOS 测试（设备基础功能）


 (并发硬件和操作系统的混乱) 测试会同时运行各种 PnP 驱动程序测试、设备驱动程序模糊测试和电源系统测试。

### <a name="span-idcoverage_testsspanspan-idcoverage_testsspanchaos-tests"></a><span id="coverage_tests"></span><span id="COVERAGE_TESTS"></span>混乱的测试

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
<td align="left"><p><span id="Disable_Enhanced_Device_Testing__EDT__Support_"></span><span id="disable_enhanced_device_testing__edt__support_"></span><span id="DISABLE_ENHANCED_DEVICE_TESTING__EDT__SUPPORT_"></span>禁用 (EDT) 支持的增强型设备测试</p></td>
<td align="left"><p>此测试会将测试筛选器驱动程序 ( # A0) 卸载为使用 DQ 参数指定的设备的上限。 此测试筛选器作为在此测试类别中运行测试的一部分进行安装</p>
<p>PnP 驱动程序测试使用 EDT 筛选器驱动程序将 IRP_MN_CANCEL_REMOVE_DEVICE 发送到目标设备堆栈。</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Run_CHAOS_Test"></span><span id="run_chaos_test"></span><span id="RUN_CHAOS_TEST"></span>运行混乱测试</p></td>
<td align="left"><p>并行运行 PnP 测试和模糊测试，同时通过所有受支持的系统电源状态循环系统。 PnP 驱动程序测试在执行 PnP 操作时向目标设备堆栈发送 i/o 请求。</p>
<p>此测试将运行 PnP 测试 (禁用/启用、重新平衡、删除/重新启动、意外删除和 DIF 删除测试设备上的) 和驱动程序模糊测试，同时在 S1、S2、S3、S4 和连接备用)  (S1、S2、S3、S4 和连接的待机状态之间循环运行测试系统。 此测试的目的是测试 PNP、i/o 和电源并发方案，并在此过程中查找任何崩溃和/或挂起。</p>
<p><strong>测试二进制文件：</strong> Devfund_ChaosTest.dll</p>
<p><strong>测试方法：</strong> RunCHAOSTest</p>
<p><strong>Parameters</strong></p>
<p><em>DQ</em> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>TestPeriod</em> - 指定以分钟)  (运行测试的时间。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](/windows-hardware/drivers)

[如何选择和配置设备基础功能测试](/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](/windows-hardware/drivers)

[PwrTest](pwrtest.md)

[渗透压力测试（设备基础功能）](penetration-tests--device-fundamentals-.md)

[PnP 测试 (设备基础) ](pnp-tests--device-fundamentals-.md)

