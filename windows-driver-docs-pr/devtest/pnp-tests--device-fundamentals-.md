---
title: PnP 测试（设备基础功能）
description: PnP 设备基础测试强制驱动程序来处理几乎所有 PnP Irp;但是，有三个区域的强调专门删除、 重新平衡和意外删除。
ms.assetid: 4224F92B-5430-4F55-900D-0B08ADBE54F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27b170a9b1e0db4666b7afe370e3b23f435e7384
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405110"
---
# <a name="pnp-tests-device-fundamentals"></a>PnP 测试（设备基础功能）


PnP 设备基础测试强制驱动程序来处理几乎所有 PnP Irp;但是，有专门强调的三个方面： 删除、 重新平衡和意外删除。 即插即用的测试提供了一种机制，测试每个单独或组合在一起对其进行测试 （即，作为压力测试中）。 此即插即用的测试被通过使用用户模式 API 调用 （通过测试应用程序） 和内核模式 （通过右上筛选器驱动程序） 的 API 调用的组合。

## <a name="pnp-tests"></a>即插即用的测试


Plug and Play (PnP) 测试在驱动程序和用户模式组件中执行各种 PnP 相关的代码路径。 即插即用的测试应运行具有[Driver Verifier](driver-verifier.md)测试计算机上启用。 有关启用驱动程序验证程序的信息，请参阅[驱动程序项目的驱动程序验证程序属性](https://msdn.microsoft.com/windows-drivers/develop/driver_verifier_properties_for__driver_projects)。

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
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP__disable_and_enable__reboot_with_IO_before_and_after"></span><span id="pnp__disable_and_enable__reboot_with_io_before_and_after"></span><span id="PNP__DISABLE_AND_ENABLE__REBOOT_WITH_IO_BEFORE_AND_AFTER"></span>重新 IO 前后的 PNP （禁用和启用） 启动</p></td>
<td align="left"><p>此测试的系统重启的设备上执行基本的即插即用禁用/启用和 I/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_PNP_DisableEnable_Reboot_With_IO_BeforeAndAfter.wsc</p>
<p><strong>测试方法：</strong>PNP_DisableEnable_Reboot_With_IO_Before_And_After</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP__disable_and_enable__with_I_O_before_and_after"></span><span id="pnp__disable_and_enable__with_i_o_before_and_after"></span><span id="PNP__DISABLE_AND_ENABLE__WITH_I_O_BEFORE_AND_AFTER"></span>之前和之后使用 I/O PNP （禁用和启用）</p></td>
<td align="left"><p>此测试可在设备上执行 I/O 和基本的即插即用禁用/启用。</p>
<p>此测试将执行以下操作：</p>
<ol>
<li>验证 reporting 设备问题代码在系统上没有任何设备。</li>
<li>使用 WDTF 简单 I/O 插件在系统上每个设备上测试 I/O。 请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh781398" data-raw-source="[Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/library/windows/hardware/hh781398)">提供 WDTF 简单 I/O 插件</a>有关详细信息。</li>
<li>禁用和启用每台设备使用 WDTF 即插即用操作接口，在系统上的看到<a href="https://msdn.microsoft.com/library/windows/hardware/hh451068" data-raw-source="[&lt;strong&gt;IWDTFPNPAction2::DisableDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451068)"> <strong>IWDTFPNPAction2::DisableDevice</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/hh451082" data-raw-source="[&lt;strong&gt;IWDTFPNPAction2::EnableDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451082)"> <strong>IWDTFPNPAction2::EnableDevice</strong> </a>方法的详细信息。</li>
<li>验证 reporting 设备问题代码在系统上没有任何设备。</li>
<li>使用 WDTF 简单 I/O 插件在系统上每个设备上测试 I/O。 请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh781398" data-raw-source="[Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/library/windows/hardware/hh781398)">提供 WDTF 简单 I/O 插件</a>有关详细信息。</li>
<li>重复步骤 3-5 几次。</li>
</ol>
<p><strong>测试二进制文件：</strong>Devfund_PNP_DisableEnable_With_IO_BeforeAndAfter.wsc</p>
<p><strong>测试方法：</strong>PNP_DisableEnable_With_IO_Before_And_After</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Cancel_Remove_Device_test_"></span><span id="pnp_cancel_remove_device_test_"></span><span id="PNP_CANCEL_REMOVE_DEVICE_TEST_"></span>即插即用取消删除设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序将 IRP_MN_CANCEL_REMOVE_DEVICE 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-device-removal-tests" data-raw-source="[About the Device Removal tests](#about-the-device-removal-tests)">有关设备删除测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPCancelRemoveDevice</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Cancel_Stop_Device_test"></span><span id="pnp_cancel_stop_device_test"></span><span id="PNP_CANCEL_STOP_DEVICE_TEST"></span>即插即用取消停止设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序将 IRP_MN_CANCEL_STOP_DEVICE 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">有关重新平衡测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPCancelStopDevice</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_DIF_Remove_Device_Test"></span><span id="pnp_dif_remove_device_test"></span><span id="PNP_DIF_REMOVE_DEVICE_TEST"></span>即插即用 DIF 删除设备测试</p></td>
<td align="left"><p>此测试使用 SetupDi API 来发送<a href="https://msdn.microsoft.com/library/windows/hardware/ff543717" data-raw-source="[&lt;strong&gt;DIF_REMOVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543717)"> <strong>DIF_REMOVE</strong> </a>要删除该设备的安装程序的请求。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPDIFRemoveAndRescanParentDevice</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Disable_and_Enable_Device_test_"></span><span id="pnp_disable_and_enable_device_test_"></span><span id="PNP_DISABLE_AND_ENABLE_DEVICE_TEST_"></span>即插即用禁用和启用设备测试</p></td>
<td align="left"><p>此测试禁用和启用的目标设备。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPDisableAndEnableDevice</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Rebalance_Fail_Restart_Device_test"></span><span id="pnp_rebalance_fail_restart_device_test"></span><span id="PNP_REBALANCE_FAIL_RESTART_DEVICE_TEST"></span>即插即用重新平衡失败重新启动设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序尝试将 IRP_MN_STOP_DEVICE 发送到目标设备堆栈。 EDT 筛选器驱动程序失败 （即按照 IRP_MN_STOP_DEVICE 请求） 执行了 IRP_MN_START_DEVICE 请求来触发目标设备被意外删除。</p>
<p>有关详细信息，请参阅<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">有关重新平衡测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPTryStopDeviceAndFailRestart</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Rebalance_Request_New_Resources_Device_test"></span><span id="pnp_rebalance_request_new_resources_device_test"></span><span id="PNP_REBALANCE_REQUEST_NEW_RESOURCES_DEVICE_TEST"></span>即插即用重新平衡请求新的资源的设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序尝试将 IRP_MN_STOP_DEVICE 发送到目标设备堆栈。 它还可操作的设备的资源要求，以最大限度地向设备分配新的资源的可能性。</p>
<p>有关详细信息，请参阅<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">有关重新平衡测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPTryStopDeviceRequestNewResourcesAndRestartDevice</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Remove_Device_Test"></span><span id="pnp_remove_device_test"></span><span id="PNP_REMOVE_DEVICE_TEST"></span>即插即用删除设备测试</p></td>
<td align="left"><p>此测试会导致 IRP_MN_QUERY_REMOVE_DEVICE 和 IRP_MN_REMOVE_DEVICE 要发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-device-removal-tests" data-raw-source="[About the Device Removal tests](#about-the-device-removal-tests)">有关设备删除测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPRemoveAndRestartDevice</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Stop__Rebalance__Device_test"></span><span id="pnp_stop__rebalance__device_test"></span><span id="PNP_STOP__REBALANCE__DEVICE_TEST"></span>即插即用 （重新平衡） 停止设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序尝试将 IRP_MN_STOP_DEVICE 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">有关重新平衡测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPTryStopAndRestartDevice</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Surprise_Remove_Device_test"></span><span id="pnp_surprise_remove_device_test"></span><span id="PNP_SURPRISE_REMOVE_DEVICE_TEST"></span>即插即用意外删除设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序将 IRP_MN_SURPRISE_REMOVAL 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-surprise-removal-test" data-raw-source="[About the Surprise Removal test](#about-the-surprise-removal-test)">有关在意外删除测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest.dll</p>
<p><strong>测试方法：</strong>PNPSurpriseRemoveAndRestartDevice</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-device-removal-tests"></a>有关设备删除测试


- 即插即用删除设备测试
- 即插即用取消删除设备测试

设备删除测试包含 IRP\_MN\_查询\_删除\_设备、 IRP\_MN\_取消\_删除\_设备和 IRP\_MN\_删除\_设备。

在测试尝试在目标设备堆栈上安装其上限的筛选器驱动程序。 此尝试会导致查询删除 IRP。

如果此查询删除 IRP 失败，测试重新启动计算机后，即可筛选器驱动程序到设备堆栈上。 如果不禁止删除请求，将删除并重新启动设备堆栈上的筛选器驱动程序设备堆栈。

测试时，通过使用安装程序 Api，将导致查询删除 IRP 发送到设备堆栈。 筛选器驱动程序失败此删除请求，以便将取消按钮删除 IRP 发送。 筛选器驱动程序将断言取消按钮删除已成功。

接下来，测试应用程序调用的相应类安装程序以及任何注册共同安装程序来禁用或启用和删除或 reenumerate 设备 (这会测试差异的类和共同安装程序处理\_与 DICSPROPERTYCHANGE\_禁用、 DICS\_启用以及 DICS\_PROPCHANGE)。 当接收 IRP\_MN\_删除\_设备，筛选器驱动程序将断言的低级驱动程序它已成功完成。

每个步骤涉及到初步删除请求。 如果该请求被否决，将不会删除设备。 您可以选择禁止删除请求，如果合适，如 USB 摄像机上的视频流式处理时或在目标设备处于启动或分页路径。 请记住，只失败的所有删除请求通常不是很好的做法。 失败的所有删除请求不会保证该驱动程序或删除 IRP 仍后将会发出在意外删除，因为如果设备堆栈中的任何人失败开始 IRP 永远不会收到删除。

## <a name="about-the-surprise-removal-test"></a>有关在意外删除测试


- 即插即用意外删除设备测试

意外删除测试包含 IRP\_MN\_惊讶\_删除后跟 IRP\_MN\_删除\_设备。

作为与以前的测试，测试应用程序将尝试将上部的筛选器添加到目标设备堆栈，然后重新启动堆栈。 如果此尝试失败，测试重新启动计算机。

当触发测试应用程序，筛选器驱动程序将会导致系统发送 IRP\_MN\_惊讶\_删除到设备堆栈中后, 跟 IRP\_MN\_删除\_设备。 筛选器驱动程序将断言，这两个这些 Irp 是已成功完成的低级驱动程序。

意外删除测试完成后，将卸载并重新枚举，该设备还从堆栈中删除筛选器驱动程序。

## <a name="about-the-rebalance-tests"></a>有关重新平衡测试


- 即插即用 （重新平衡） 停止设备测试
- 即插即用重新平衡请求新的资源的设备测试
- 即插即用重新平衡失败重新启动设备测试
- 即插即用取消停止设备测试

如删除测试，测试应用程序将尝试将上部的筛选器添加到目标设备堆栈和使用，然后重新启动设备堆栈**SetupDiCallClassInstaller**与 DIF\_PROPERTYCHANGE。 如果此尝试不成功 （即，如果有人在目标设备堆栈失败查询删除 IRP），测试会重新启动计算机，以测试重新平衡。

根据重新平衡测试的选择，将发生以下事件：

1.  **即插即用 （重新平衡） 停止设备测试**此测试启动的重新平衡过程，这会导致 IRP\_MN\_查询\_停止\_设备 PnP IRP 设备驱动程序。

    如果堆栈中的任何驱动程序无法重新均衡过程已放弃此 IRP 正常工作。 请注意，Windows Vista 中，支持多级别重新平衡。 如果在非叶设备节点上启动时再平衡，则所有与该设备节点为根设备树中存在的设备堆栈也要经历重新平衡中。 如果任何子设备堆栈失败查询停止，放弃整个重新平衡过程。 因此，驱动程序必须不失败而无需真正的理由，否则查询停止。 如果发生此故障，即插即用管理器发送取消停止 (IRP\_MN\_取消\_停止) 到已发送查询停止的所有设备堆栈。

    如果设备堆栈所涉及的所有通过查询停止，测试将继续执行重新平衡，并将发送 IRP\_MN\_查询\_资源\_要求和 IRP\_MN\_筛选器\_资源\_要求 IRP，若要查找的设备的资源要求。

    此点之后，则具体取决于是否在目标设备会占用任何资源或不可能发生两种不同方法：

    -   如果设备不占用任何资源，即插即用的管理器本身将发送一个取消停止 (IRP\_MN\_取消\_停止\_设备) 作为一种优化。

        如果设备实际使用的资源，重新平衡过程已完成并且 IRP\_MN\_停止\_设备和 IRP\_MN\_启动\_设备 Irp。

    使用此选项时，不要更改设备的资源。

2.  **即插即用取消停止设备测试**:此测试启动重新平衡过程中，但筛选器驱动程序有意失败查询停止 IRP。 Irp 的顺序如下所示 IRP\_MN\_查询\_停止\_设备 （这由筛选器驱动程序时启动，从而导致取消重新平衡即将发布失败） 和 IRP\_MN\_取消\_停止\_设备。

    使用此选项时，设备的资源不会更改

3.  **即插即用重新平衡请求新的资源的设备测试**此测试启动再平衡，并还操作设备的资源要求，以最大程度提高真正新的资源分配给该设备的可能性。 此选项还有助于通过完成重新平衡过程切实采取任何资源的设备：
    1.  首次启动简单重新平衡，从而导致以下 Irp:
        -   IRP\_MN\_查询\_停止\_设备 （假设此 IRP 传递的所有驱动程序。 测试已涵盖此 IRP 失败的情况。）
        -   IRP\_MN\_查询\_资源\_要求
        -   IRP\_MN\_筛选器\_资源\_要求。 在响应时，将此 IRP，筛选器驱动程序采用基于设备是否在或不使用任何资源的操作：
            -   如果设备没有任何资源要求，筛选器将分配虚设的资源。
            -   如果设备有资源要求，它将尝试进行重组的资源要求列表中的方式来最大化更改当前分配的概率。 例如，如果设备需要 2 个字节的内存 00 到 FF 之间的任意位置，并且当前分配 3A 3B，修改，以便 （按优先顺序） 的新资源要求如下所示 00-39 或 3 C FF 或 3A 3B。 同样如果设备资源要求列表不包含任何备用的要求，它将更改其顺序，以便备用需求来自前面的列表。

    2.  现在设备应始终完成重新平衡过程。

        IRP\_MN\_STOP\_DEVICE

        IRP\_MN\_启动\_设备 （新的已分配资源。 如果创建了假的要求，屏蔽从实际的驱动程序的新资源。）

4.  **即插即用重新平衡失败重新启动设备测试**此测试启动再平衡，但当筛选器驱动程序后重新平衡获取开始，它有意失败 it 这会导致意外删除 IRP 后, 跟删除 IRP。

    首先，它会启动重新平衡过程，并可确保该驱动程序获取停止和启动，通过生成不占用任何资源的设备的虚设资源要求。

    -   IRP\_MN\_查询\_停止\_设备 （假设此 IRP 传递的所有驱动程序。 测试已涵盖此 IRP 失败的情况。）
    -   IRP\_MN\_查询\_资源\_要求
    -   IRP\_MN\_筛选器\_资源\_要求 （如果实际资源要求都为 null，筛选器分配假资源要求，因此没有停止和启动。）
    -   IRP\_MN\_STOP\_DEVICE
    -   IRP\_MN\_启动\_设备 （筛选器失败时将启动此 IRP。 此操作将导致意外删除 IRP。）
    -   IRP\_MN\_SURPRISE\_REMOVAL
    -   IRP\_MN\_REMOVE

    重新平衡测试完成后，将卸载并重新枚举，该设备还从堆栈中删除筛选器驱动程序。

## <a name="device-error-codes"></a>设备错误代码


如果测试显示错误消息，指出设备状态不正常，您可以详细了解设备状态通过设备管理器。 有关的各种设备错误代码，请参阅[设备管理器错误消息](https://msdn.microsoft.com/library/windows/hardware/ff541422)。

## <a name="debug-installation-failures-using-the-setup-api-logs"></a>调试使用安装程序 API 日志的安装失败


安装程序 API 日志 （setupapi.app.log 和 setupapi.dev.log） 可能包含有用的信息来调试记录此测试的驱动程序安装失败。 安装程序 API 日志可以位于 %windir%\\inf\\目录上的测试系统。

若要增加详细级别和潜在有效性这些日志，请重新安装测试之前的以下注册表项设置为 0x2000FFFF:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="related-topics"></a>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-select-and-configure-the-device-fundamental-tests)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/library/windows/hardware/hh781398)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 






