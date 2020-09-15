---
title: ProcAmp 控制的示例函数
description: ProcAmp 控制的示例函数
ms.assetid: d158216e-9a34-48a4-adca-e3c20b5e4487
keywords:
- ProcAmp WDK DirectX VA，示例函数
- 范围 WDK ProcAmp
- 属性 WDK ProcAmp
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aee2d5ddb4447d4f9c765a307002e2a54f4a8b23
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104692"
---
# <a name="sample-functions-for-procamp-control"></a>ProcAmp 控制的示例函数


## <span id="ddk_sample_functions_for_procamp_control_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_PROCAMP_CONTROL_GG"></span>


本部分中的示例 ProcAmp 函数演示如何实现 ProcAmp 控件功能。 这些示例函数映射到[**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构中定义的[运动补偿回调函数](motion-compensation-callbacks.md)。 您可以实现每个示例函数，然后使用运动补偿代码模板来完成实现。 有关详细信息，请参阅 [DIRECTX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

### <a name="span-iddeinterlace_container_device_class_sample_functionsspanspan-iddeinterlace_container_device_class_sample_functionsspanspan-iddeinterlace_container_device_class_sample_functionsspandeinterlace-container-device-class-sample-functions"></a><span id="Deinterlace_Container_Device_Class_Sample_Functions"></span><span id="deinterlace_container_device_class_sample_functions"></span><span id="DEINTERLACE_CONTAINER_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>隔行扫描容器设备类示例函数

下表中的示例 ProcAmp 控制函数是 *DXVA \_ DeinterlaceContainerDeviceClass* (的成员函数，也就是说，使用隔行扫描容器设备) 调用它们。 有关详细信息，请参阅 [定义隔行扫描容器设备类](defining-the-deinterlace-container-device-class.md) 和 [执行 ProcAmp Control 和取消隔行扫描操作](performing-procamp-control-and-deinterlacing-operations.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryCaps&lt;/strong&gt;](./dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)"><strong>ProcAmpControlQueryCaps</strong></a></p></td>
<td align="left"><p>查询驱动程序以确定 ProcAmp 控制设备的输入要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryRange&lt;/strong&gt;](./dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)"><strong>ProcAmpControlQueryRange</strong></a></p></td>
<td align="left"><p>查询驱动程序以确定每个 ProcAmp 属性的最小值、最大值、步长大小和默认值。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idprocamp_control_device_class_sample_functionsspanspan-idprocamp_control_device_class_sample_functionsspanspan-idprocamp_control_device_class_sample_functionsspanprocamp-control-device-class-sample-functions"></a><span id="ProcAmp_Control_Device_Class_Sample_Functions"></span><span id="procamp_control_device_class_sample_functions"></span><span id="PROCAMP_CONTROL_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>ProcAmp 控件设备类示例函数

下表中的示例 ProcAmp 控制函数是 *DXVA \_ ProcAmpControlDeviceClass* (的成员函数，也就是说，它们是使用 ProcAmp 控制设备) 调用的。 有关详细信息，请参阅 [定义 ProcAmp 控件设备类](defining-the-procamp-control-device-class.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream" data-raw-source="[&lt;strong&gt;ProcAmpControlOpenStream&lt;/strong&gt;](./dxva-procampcontroldeviceclass-procampcontrolopenstream.md)"><strong>ProcAmpControlOpenStream</strong></a></p></td>
<td align="left"><p>创建 ProcAmp 流对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt" data-raw-source="[&lt;strong&gt;ProcAmpControlBlt&lt;/strong&gt;](./dxva-procampcontroldeviceclass-procampcontrolblt.md)"><strong>ProcAmpControlBlt</strong></a></p></td>
<td align="left"><p>通过将输出写入目标图面来执行 ProcAmp 调整操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream" data-raw-source="[&lt;strong&gt;ProcAmpControlCloseStream&lt;/strong&gt;](./dxva-procampcontroldeviceclass-procampcontrolclosestream.md)"><strong>ProcAmpControlCloseStream</strong></a></p></td>
<td align="left"><p>关闭 ProcAmp 流对象，并指示设备驱动程序释放与该流关联的硬件资源。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmapping_sample_functions_to_dd_motioncompcallbacksspanspan-idmapping_sample_functions_to_dd_motioncompcallbacksspanspan-idmapping_sample_functions_to_dd_motioncompcallbacksspanmapping-sample-functions-to-dd_motioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>将示例函数映射到 DD \_ MOTIONCOMPCALLBACKS

本节中的示例函数将映射到运动补偿回调函数，如下所示。 也就是说，每个示例函数在其各自的运动补偿回调中调用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">DD_MOTIONCOMPCALLBACKS 成员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryCaps&lt;/strong&gt;](./dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)"><strong>ProcAmpControlQueryCaps</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryRange&lt;/strong&gt;](./dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)"><strong>ProcAmpControlQueryRange</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream" data-raw-source="[&lt;strong&gt;ProcAmpControlOpenStream&lt;/strong&gt;](./dxva-procampcontroldeviceclass-procampcontrolopenstream.md)"><strong>ProcAmpControlOpenStream</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt" data-raw-source="[&lt;strong&gt;ProcAmpControlBlt&lt;/strong&gt;](./dxva-procampcontroldeviceclass-procampcontrolblt.md)"><strong>ProcAmpControlBlt</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream" data-raw-source="[&lt;strong&gt;ProcAmpControlCloseStream&lt;/strong&gt;](./dxva-procampcontroldeviceclass-procampcontrolclosestream.md)"><strong>ProcAmpControlCloseStream</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

