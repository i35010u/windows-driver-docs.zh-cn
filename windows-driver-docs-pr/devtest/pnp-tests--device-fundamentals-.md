---
title: PnP 测试（设备基础功能）
description: 设备基础知识 PnP 测试强制驱动程序处理几乎所有 PnP Irp;但是，有三个方面会特别删除、重新均衡和意外删除。
ms.assetid: 4224F92B-5430-4F55-900D-0B08ADBE54F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61f6b6db5523925a4e8d3514e5f540e54111cd26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840056"
---
# <a name="pnp-tests-device-fundamentals"></a>PnP 测试（设备基础功能）


设备基础知识 PnP 测试强制驱动程序处理几乎所有 PnP Irp;不过，有三个区域特别明显：删除、重新平衡和意外删除。 PnP 测试提供一种机制来单独测试每个测试，或将它们一起测试（即，作为压力测试）。 此 PnP 测试通过结合使用用户模式 API 调用（通过测试应用程序）和内核模式 API 调用（通过上限筛选器驱动程序）来实现。

## <a name="pnp-tests"></a>PNP 测试


即插即用（PnP）测试在驱动程序和用户模式组件中执行各种与 PnP 相关的代码路径。 PnP 测试应在测试计算机上启用了[驱动程序验证程序](driver-verifier.md)的情况运行。 有关启用驱动程序验证程序的信息，请参阅驱动程序[项目的驱动程序验证程序属性](https://docs.microsoft.com/windows-hardware/drivers)。

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
<td align="left"><p><span id="Disable_Enhanced_Device_Testing__EDT__Support_"></span><span id="disable_enhanced_device_testing__edt__support_"></span><span id="DISABLE_ENHANCED_DEVICE_TESTING__EDT__SUPPORT_"></span>禁用增强型设备测试（EDT）支持</p></td>
<td align="left"><p>此测试将测试筛选器驱动程序（msdmfilt）卸载为使用 DQ 参数指定的设备的上限。 此测试筛选器作为在此测试类别中运行测试的一部分进行安装</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP__disable_and_enable__reboot_with_IO_before_and_after"></span><span id="pnp__disable_and_enable__reboot_with_io_before_and_after"></span><span id="PNP__DISABLE_AND_ENABLE__REBOOT_WITH_IO_BEFORE_AND_AFTER"></span>PNP （禁用和启用）使用 IO 在之前和之后重新启动</p></td>
<td align="left"><p>此测试在系统重新启动时在设备上执行基本的 PnP 禁用/启用和 i/o。</p>
<p><strong>测试二进制文件：</strong>Devfund_PNP_DisableEnable_Reboot_With_IO_BeforeAndAfter. wsc</p>
<p><strong>测试方法：</strong>PNP_DisableEnable_Reboot_With_IO_Before_And_After</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP__disable_and_enable__with_I_O_before_and_after"></span><span id="pnp__disable_and_enable__with_i_o_before_and_after"></span><span id="PNP__DISABLE_AND_ENABLE__WITH_I_O_BEFORE_AND_AFTER"></span>PNP （禁用和启用）和前后的 i/o</p></td>
<td align="left"><p>此测试在设备上执行 i/o 和基本 PnP 禁用/启用。</p>
<p>此测试执行以下操作：</p>
<ol>
<li>验证系统报告设备问题代码上是否没有设备。</li>
<li>使用 WDTF 简单 i/o 插件测试系统上每台设备上的 i/o。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins" data-raw-source="[Provided WDTF Simple I/O plug-ins](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)">提供的 WDTF 简单 i/o 插件</a>。</li>
<li>使用 WDTF PnP 操作接口禁用和启用系统上的每个设备，有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-disabledevice" data-raw-source="[&lt;strong&gt;IWDTFPNPAction2::DisableDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-disabledevice)"><strong>IWDTFPNPAction2：:D isabledevice</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-enabledevice" data-raw-source="[&lt;strong&gt;IWDTFPNPAction2::EnableDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-enabledevice)"><strong>IWDTFPNPAction2：： EnableDevice</strong></a>方法。</li>
<li>验证系统报告设备问题代码上是否没有设备。</li>
<li>使用 WDTF 简单 i/o 插件测试系统上每台设备上的 i/o。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins" data-raw-source="[Provided WDTF Simple I/O plug-ins](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)">提供的 WDTF 简单 i/o 插件</a>。</li>
<li>多次重复步骤3-5。</li>
</ol>
<p><strong>测试二进制文件：</strong>Devfund_PNP_DisableEnable_With_IO_BeforeAndAfter. wsc</p>
<p><strong>测试方法：</strong>PNP_DisableEnable_With_IO_Before_And_After</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Cancel_Remove_Device_test_"></span><span id="pnp_cancel_remove_device_test_"></span><span id="PNP_CANCEL_REMOVE_DEVICE_TEST_"></span>PNP 取消删除设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序将 IRP_MN_CANCEL_REMOVE_DEVICE 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-device-removal-tests" data-raw-source="[About the Device Removal tests](#about-the-device-removal-tests)">关于设备删除测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPCancelRemoveDevice</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Cancel_Stop_Device_test"></span><span id="pnp_cancel_stop_device_test"></span><span id="PNP_CANCEL_STOP_DEVICE_TEST"></span>PNP 取消停止设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序将 IRP_MN_CANCEL_STOP_DEVICE 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">关于重新平衡测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPCancelStopDevice</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_DIF_Remove_Device_Test"></span><span id="pnp_dif_remove_device_test"></span><span id="PNP_DIF_REMOVE_DEVICE_TEST"></span>PNP DIF 删除设备测试</p></td>
<td align="left"><p>此测试使用 SetupDi API 向安装程序发送<a href="https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove" data-raw-source="[&lt;strong&gt;DIF_REMOVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove)"><strong>DIF_REMOVE</strong></a>请求以删除设备。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPDIFRemoveAndRescanParentDevice</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Disable_and_Enable_Device_test_"></span><span id="pnp_disable_and_enable_device_test_"></span><span id="PNP_DISABLE_AND_ENABLE_DEVICE_TEST_"></span>PNP 禁用和启用设备测试</p></td>
<td align="left"><p>此测试将禁用并启用目标设备。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPDisableAndEnableDevice</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Rebalance_Fail_Restart_Device_test"></span><span id="pnp_rebalance_fail_restart_device_test"></span><span id="PNP_REBALANCE_FAIL_RESTART_DEVICE_TEST"></span>PNP 重新平衡失败重新启动设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序尝试将 IRP_MN_STOP_DEVICE 发送到目标设备堆栈。 然后，EDT 筛选器驱动程序会使 IRP_MN_START_DEVICE 请求（遵循 IRP_MN_STOP_DEVICE 请求）触发对目标设备的意外删除。</p>
<p>有关详细信息，请参阅<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">关于重新平衡测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPTryStopDeviceAndFailRestart</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Rebalance_Request_New_Resources_Device_test"></span><span id="pnp_rebalance_request_new_resources_device_test"></span><span id="PNP_REBALANCE_REQUEST_NEW_RESOURCES_DEVICE_TEST"></span>PNP 重新平衡请求新资源设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序尝试将 IRP_MN_STOP_DEVICE 发送到目标设备堆栈。 它还处理设备的资源要求，以最大限度地将新资源分配给设备的机会。</p>
<p>有关详细信息，请参阅<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">关于重新平衡测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPTryStopDeviceRequestNewResourcesAndRestartDevice</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Remove_Device_Test"></span><span id="pnp_remove_device_test"></span><span id="PNP_REMOVE_DEVICE_TEST"></span>PNP 删除设备测试</p></td>
<td align="left"><p>此测试将导致 IRP_MN_QUERY_REMOVE_DEVICE 和 IRP_MN_REMOVE_DEVICE 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-device-removal-tests" data-raw-source="[About the Device Removal tests](#about-the-device-removal-tests)">关于设备删除测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPRemoveAndRestartDevice</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Stop__Rebalance__Device_test"></span><span id="pnp_stop__rebalance__device_test"></span><span id="PNP_STOP__REBALANCE__DEVICE_TEST"></span>PNP 停止（重新平衡）设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序尝试将 IRP_MN_STOP_DEVICE 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">关于重新平衡测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPTryStopAndRestartDevice</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Surprise_Remove_Device_test"></span><span id="pnp_surprise_remove_device_test"></span><span id="PNP_SURPRISE_REMOVE_DEVICE_TEST"></span>PNP 意外删除设备测试</p></td>
<td align="left"><p>此测试使用 EDT 筛选器驱动程序将 IRP_MN_SURPRISE_REMOVAL 发送到目标设备堆栈。</p>
<p>有关详细信息，请参阅<a href="#about-the-surprise-removal-test" data-raw-source="[About the Surprise Removal test](#about-the-surprise-removal-test)">关于意外删除测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_PnPDTest</p>
<p><strong>测试方法：</strong>PNPSurpriseRemoveAndRestartDevice</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-device-removal-tests"></a>关于设备删除测试


- PNP 删除设备测试
- PNP 取消删除设备测试

设备删除测试包含 IRP\_MN\_QUERY\_删除\_设备、IRP\_MN\_取消\_删除\_设备以及 IRP\_MN\_删除\_设备。

测试尝试在目标设备堆栈上安装其高层筛选器驱动程序。 此尝试将导致查询删除 IRP。

如果此查询-remove IRP 失败，则测试将重新启动计算机，以使筛选器驱动程序进入设备堆栈。 如果删除请求不是否决的，则设备堆栈将被删除，并将筛选器驱动程序重启到设备堆栈上。

通过使用安装 Api，测试会导致将查询删除 IRP 发送到设备堆栈。 筛选器驱动程序未通过此删除请求，因此发送了取消删除 IRP。 筛选器驱动程序将断言取消删除操作成功。

接下来，测试应用程序将调用相应的类安装程序和任何已注册的联合安装程序，以禁用或启用和 reenumerate 设备（这会测试与 DICS\_的 DIF\_PROPERTYCHANGE 的类和共同安装程序处理。DISABLE、DICS\_ENABLE 和 DICS\_PROPCHANGE）。 接收 IRP\_MN 时\_删除\_设备，筛选器驱动程序将断言该驱动程序的驱动程序已成功完成。

其中每个步骤都涉及一个初步删除请求。 如果拒绝该请求，则不会删除设备。 你可以选择在适当的时候拒绝删除请求，例如，当在 USB 摄像机上流式传输视频时，或者目标设备处于启动或寻呼路径时。 请记住，仅当所有删除请求失败时，通常不是很好的做法。 如果失败所有删除请求，则无法保证驱动程序永远不会收到删除，因为删除 IRP 仍将在意外删除后发出，或者设备堆栈中的任何人都无法启动 IRP。

## <a name="about-the-surprise-removal-test"></a>关于意外删除测试


- PNP 意外删除设备测试

意外删除测试包含 IRP\_MN\_意外\_删除，然后 IRP\_MN\_删除\_设备。

与前面的测试一样，测试应用程序将尝试向目标设备堆栈添加一个上限筛选器，然后重新启动堆栈。 如果此尝试不成功，则测试将重新启动计算机。

由测试应用程序触发时，筛选器驱动程序将导致系统将 IRP\_MN 发送到设备堆栈\_意外\_删除，后跟 IRP\_MN\_删除\_设备。 筛选器驱动程序将断言这些 Irp 都已由较低的驱动程序成功完成。

意外删除测试完成后，设备将被卸载并 reenumerated，同时从堆栈中删除筛选器驱动程序。

## <a name="about-the-rebalance-tests"></a>关于重新平衡测试


- PNP 停止（重新平衡）设备测试
- PNP 重新平衡请求新资源设备测试
- PNP 重新平衡失败重新启动设备测试
- PNP 取消停止设备测试

与删除测试一样，测试应用程序会尝试向目标设备堆栈添加上限筛选器，然后通过将**SetupDiCallClassInstaller**与 DIF\_PROPERTYCHANGE 配合使用来重新启动设备堆栈。 如果此尝试不成功（即，如果目标设备堆栈上的某个用户未能通过查询-删除 IRP），则测试将重新启动计算机以测试重新平衡。

根据所选的重新均衡测试，会发生以下事件：

1.  **PNP 停止（重新平衡）设备测试**此测试将启动重新平衡过程，这将导致 IRP\_MN\_QUERY\_停止\_设备驱动程序的设备 PnP IRP。

    如果堆栈中的任何驱动程序失败，则放弃重新平衡过程。 请注意，在 Windows Vista 中，支持多层重新平衡。 如果在非叶设备节点上启动重新平衡，则设备树中出现的设备堆栈（该设备节点作为根）也会经历重新平衡。 如果任何子设备堆栈未能通过查询停止，则会放弃整个重新平衡过程。 因此，在没有真正原因的情况下，驱动程序不能使查询停止失败。 如果发生此错误，PnP 管理器会向已发送查询停止的所有设备堆栈发送取消停止（IRP\_MN\_取消\_停止）。

    如果涉及的所有设备堆栈都传递查询停止，则测试将继续进行重新平衡，并将 IRP\_MN\_查询\_资源\_要求和 IRP\_\_\_筛选器\_资源IRP 来查找设备的资源要求。

    在此之后，根据目标设备是否使用任何资源，可能有两种不同的路径：

    -   如果设备不消耗任何资源，则 "PnP 管理器" 会自行发送取消停止（IRP\_MN\_CANCEL\_STOP\_设备）作为优化。

        如果设备实际消耗资源，则使用 IRP\_MN\_停止\_设备和 IRP\_MN\_启动\_设备 Irp 来完成重新平衡过程。

    如果选择此选项，则不会更改设备的资源。

2.  **PNP 取消停止设备测试**：此测试启动重新平衡过程，但筛选器驱动程序特意失败查询停止 IRP。 Irp 的顺序看起来像 IRP\_MN\_QUERY\_停止\_设备（此操作在启动时筛选器驱动程序失败，导致取消重新平衡）和 IRP\_MN\_取消\_停止\_装置.

    如果选择此选项，则不会更改设备的资源

3.  **PNP 重新平衡请求新资源设备测试**此测试将启动重新平衡，并处理设备的资源要求，从而最大限度地提高将实际新资源分配给设备的机会。 此选项还有助于无资源的设备真正完成重新平衡过程：
    1.  首先启动简单的重新平衡，导致以下 Irp：
        -   IRP\_MN\_QUERY\_停止\_设备（假定所有驱动程序都传递此 IRP。 此测试已覆盖此 IRP 失败的情况。）
        -   IRP\_MN\_查询\_资源\_要求
        -   IRP\_MN\_筛选\_资源\_要求。 在进行此 IRP 时，筛选器驱动程序会根据设备是否使用任何资源来执行操作：
            -   如果设备没有资源要求，则筛选器将分配一个虚设资源。
            -   如果设备有资源要求，它会尝试以这样一种方式重构资源需求列表，以最大程度地提高更改当前分配的概率。 例如，如果设备需要在00到 FF 之间的任何位置使用2个字节的内存，并且当前分配了 3A-3B，请修改新资源需求（按优先顺序排列），使其看起来像00-39 或 3C-FF 或 3A-3B。 同样，如果设备资源要求列表具有任何备用要求，则会更改其顺序，以便在列表中提前出现备用要求。

    2.  现在，设备应始终完成重新平衡过程。

        IRP\_MN\_停止\_设备

        IRP\_MN\_启动\_设备（新分配的资源。 如果创建了假要求，请从实际驱动程序中屏蔽新资源。）

4.  **PNP 重新平衡失败重新启动设备测试**此测试将启动重新平衡，但当筛选器驱动程序在重新平衡后获取开始时，它会有意失败，这会导致意外删除 IRP，然后删除 IRP。

    首先，它会启动重新平衡过程，并确保驱动程序通过为不占用任何资源的设备生成虚假资源需求来实现停止和启动。

    -   IRP\_MN\_QUERY\_停止\_设备（假定所有驱动程序都传递此 IRP。 此测试已覆盖此 IRP 失败的情况。）
    -   IRP\_MN\_查询\_资源\_要求
    -   IRP\_MN\_筛选\_资源\_要求（如果实际资源需求为 null，筛选器分配虚假资源要求，因此存在停止和开始。）
    -   IRP\_MN\_停止\_设备
    -   IRP\_MN\_启动\_设备（在此之后，筛选器将会失败。 此操作会导致意外的删除 IRP。）
    -   IRP\_MN\_意外\_删除
    -   IRP\_MN\_删除

    重新平衡测试完成后，设备将被卸载并 reenumerated，同时还会从堆栈中删除筛选器驱动程序。

## <a name="device-error-codes"></a>设备错误代码


如果测试发出错误消息，指出设备状态不正常，可以通过设备管理器了解有关设备状态的详细信息。 有关各种设备错误代码的摘要，请参阅[设备管理器错误消息](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)。

## <a name="debug-installation-failures-using-the-setup-api-logs"></a>使用安装程序 API 日志调试安装失败


安装 API 日志（setupapi.log 和 setupapi.log）可能包含有用的信息，可用于调试此测试记录的驱动程序安装失败。 可在测试系统上的% windir%\\inf\\ 目录下找到安装程序 API 日志。

若要提高这些日志的详细程度和潜在有用性，请在运行重新安装测试之前，将以下注册表项设置为0x2000FFFF：

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="related-topics"></a>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-select-and-configure-the-device-fundamental-tests)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](https://docs.microsoft.com/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

 

 






