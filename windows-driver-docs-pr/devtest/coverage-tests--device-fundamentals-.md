---
title: 覆盖范围测试（设备基础功能）
description: 设备基础覆盖率测试监视和报告各种 i/o 请求数据包 (Irp) 为指定设备进入或离开驱动程序堆栈。
ms.assetid: 950B124B-8B2D-4A54-AFC3-E90BBDD8D1AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a9aff4611a03def9824a6e0f82d4d90323d35f1
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383729"
---
# <a name="coverage-tests-device-fundamentals"></a>覆盖范围测试（设备基础功能）


设备基础覆盖率测试监视和报告各种 i/o 请求数据包 (Irp) 为指定设备进入或离开驱动程序堆栈。 覆盖率测试中的数据可帮助确定驱动程序测试和验证过程中的覆盖率弱点。

### <a name="span-idcoverage_testsspanspan-idcoverage_testsspancoverage-tests"></a><span id="coverage_tests"></span><span id="COVERAGE_TESTS"></span>覆盖率测试

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
<td align="left"><p><span id="Clear_IRP_coverage_data_"></span><span id="clear_irp_coverage_data_"></span><span id="CLEAR_IRP_COVERAGE_DATA_"></span>清除 IRP 覆盖率数据</p></td>
<td align="left"><p>清除 IRP 覆盖率数据。</p>
<p><strong>测试二进制文件：</strong> DriverCoverageClearCoverageData.dll</p>
<p><strong>测试方法：</strong> ClearCoverageData</p>
<p><strong>参数：</strong>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Disable_IRP_coverage_data_collection"></span><span id="disable_irp_coverage_data_collection"></span><span id="DISABLE_IRP_COVERAGE_DATA_COLLECTION"></span>禁用 IRP 覆盖率数据收集</p></td>
<td align="left"><p>禁用由 <em>DQ</em> 参数指定的设备的 IRP 覆盖率数据收集。</p>
<p><strong>测试二进制文件：</strong> DriverCoverageDisableSupport.dll</p>
<p><strong>测试方法：</strong> DisableCoverageDataCollection</p>
<p><strong>Parameters</strong></p>
<p><em>DQ</em> - 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Display_collected_IRP_coverage_data._"></span><span id="display_collected_irp_coverage_data._"></span><span id="DISPLAY_COLLECTED_IRP_COVERAGE_DATA._"></span>显示收集的 IRP 覆盖率数据。</p></td>
<td align="left"><p>显示为所有设备收集到此点的 IRP 覆盖率数据。</p>
<p><strong>测试二进制文件：</strong> DriverCoverageDisplayCoverage.dll</p>
<p><strong>测试方法：</strong> DisplayCoverageData</p>
<p><strong>参数：</strong>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_IRP_coverage_enabled_devices"></span><span id="display_irp_coverage_enabled_devices"></span><span id="DISPLAY_IRP_COVERAGE_ENABLED_DEVICES"></span>显示启用 IRP 覆盖区的设备</p></td>
<td align="left"><p>显示当前为其启用 IRP 覆盖率数据收集的设备。</p>
<p><strong>测试二进制文件：</strong> DriverCoverageDisplayEnabledDevices.dll</p>
<p><strong>测试方法：</strong> DisplayEnabledDevices</p>
<p><strong>参数：</strong>无</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_IRP_coverage_data_collection"></span><span id="enable_irp_coverage_data_collection"></span><span id="ENABLE_IRP_COVERAGE_DATA_COLLECTION"></span>启用 IRP 覆盖率数据收集</p></td>
<td align="left"><p>为 <em>DQ</em> 参数指定的设备启用 IRP 覆盖率数据收集。</p>
<p><strong>测试二进制文件：</strong> DriverCoverageEnableSupport.dll</p>
<p><strong>测试方法：</strong> EnableCoverageDataCollection</p>
<p><strong>参数：</strong>无</p>
<p><em>DQ</em> - 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idabout_the_coverage_testsspanspan-idabout_the_coverage_testsspanspan-idabout_the_coverage_testsspanabout-the-coverage-tests"></a><span id="About_the_Coverage_tests"></span><span id="about_the_coverage_tests"></span><span id="ABOUT_THE_COVERAGE_TESTS"></span>关于覆盖率测试

设备基础覆盖率测试基于驱动程序覆盖套件，该工具包以前在 WDK 中作为独立工具提供。 有关如何实现覆盖率测试的信息，请参阅 [驱动程序覆盖率工具包](driver-coverage-toolkit.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](/windows-hardware/drivers)

[如何选择和配置设备基础功能测试](/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](../wdtf/provided-wdtf-simpleio-plug-ins.md)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](/windows-hardware/drivers)

 

