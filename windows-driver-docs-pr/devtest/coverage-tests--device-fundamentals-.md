---
title: 覆盖范围测试（设备基础功能）
description: 设备基本覆盖率测试监视和报告的各种 I/O 请求数据包 (Irp)，进入或离开指定设备驱动程序堆栈。
ms.assetid: 950B124B-8B2D-4A54-AFC3-E90BBDD8D1AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08e5da67ea719cc004a8414e224532bc597daa04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343107"
---
# <a name="coverage-tests-device-fundamentals"></a>覆盖范围测试（设备基础功能）


设备基本覆盖率测试监视和报告的各种 I/O 请求数据包 (Irp)，进入或离开指定设备驱动程序堆栈。 从覆盖率测试数据可帮助标识驱动程序测试和验证过程中的覆盖率的弱点。

### <a name="span-idcoveragetestsspanspan-idcoveragetestsspancoverage-tests"></a><span id="coverage_tests"></span><span id="COVERAGE_TESTS"></span>覆盖率测试

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
<td align="left"><p><span id="Clear_IRP_coverage_data_"></span><span id="clear_irp_coverage_data_"></span><span id="CLEAR_IRP_COVERAGE_DATA_"></span>清除 IRP 覆盖率数据</p></td>
<td align="left"><p>清除 IRP 覆盖率数据。</p>
<p><strong>测试二进制文件：</strong>DriverCoverageClearCoverageData.dll</p>
<p><strong>测试方法：</strong>ClearCoverageData</p>
<p><strong>参数：</strong>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Disable_IRP_coverage_data_collection"></span><span id="disable_irp_coverage_data_collection"></span><span id="DISABLE_IRP_COVERAGE_DATA_COLLECTION"></span>禁用 IRP 覆盖率数据集合</p></td>
<td align="left"><p>禁用指定设备的 IRP 覆盖率数据集合<em>DQ</em>参数。</p>
<p><strong>测试二进制文件：</strong>DriverCoverageDisableSupport.dll</p>
<p><strong>测试方法：</strong>DisableCoverageDataCollection</p>
<p><strong>参数：</strong></p>
<p><em>DQ</em> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Display_collected_IRP_coverage_data._"></span><span id="display_collected_irp_coverage_data._"></span><span id="DISPLAY_COLLECTED_IRP_COVERAGE_DATA._"></span>显示收集的 IRP 覆盖率数据。</p></td>
<td align="left"><p>显示 IRP 覆盖率数据收集到目前为止的所有设备。</p>
<p><strong>测试二进制文件：</strong>DriverCoverageDisplayCoverage.dll</p>
<p><strong>测试方法：</strong>DisplayCoverageData</p>
<p><strong>参数：</strong>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_IRP_coverage_enabled_devices"></span><span id="display_irp_coverage_enabled_devices"></span><span id="DISPLAY_IRP_COVERAGE_ENABLED_DEVICES"></span>启用设备显示 IRP 覆盖率</p></td>
<td align="left"><p>显示当前已为其启用 IRP 覆盖率数据集合的设备。</p>
<p><strong>测试二进制文件：</strong>DriverCoverageDisplayEnabledDevices.dll</p>
<p><strong>测试方法：</strong>DisplayEnabledDevices</p>
<p><strong>参数：</strong>无</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_IRP_coverage_data_collection"></span><span id="enable_irp_coverage_data_collection"></span><span id="ENABLE_IRP_COVERAGE_DATA_COLLECTION"></span>启用 IRP 覆盖率数据集合</p></td>
<td align="left"><p>启用指定的设备的 IRP 覆盖率数据收集<em>DQ</em>参数。</p>
<p><strong>测试二进制文件：</strong>DriverCoverageEnableSupport.dll</p>
<p><strong>测试方法：</strong>EnableCoverageDataCollection</p>
<p><strong>参数：</strong>无</p>
<p><em>DQ</em> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idaboutthecoveragetestsspanspan-idaboutthecoveragetestsspanspan-idaboutthecoveragetestsspanabout-the-coverage-tests"></a><span id="About_the_Coverage_tests"></span><span id="about_the_coverage_tests"></span><span id="ABOUT_THE_COVERAGE_TESTS"></span>有关覆盖率测试

设备基础覆盖率测试取决于驱动程序覆盖范围工具包，这是以前可用作独立工具在 WDK 中。 有关如何实现覆盖率测试的信息，请参阅[驱动程序覆盖范围工具包](driver-coverage-toolkit.md)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/library/windows/hardware/hh781398)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 






