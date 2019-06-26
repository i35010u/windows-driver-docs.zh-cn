---
title: ProcAmp 控制的示例函数
description: ProcAmp 控制的示例函数
ms.assetid: d158216e-9a34-48a4-adca-e3c20b5e4487
keywords:
- ProcAmp WDK DirectX va，因此示例函数
- WDK ProcAmp 范围
- WDK ProcAmp 属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c4bd5008278cdfd1f355e6742ebc88b6700ea4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365577"
---
# <a name="sample-functions-for-procamp-control"></a>ProcAmp 控制的示例函数


## <span id="ddk_sample_functions_for_procamp_control_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_PROCAMP_CONTROL_GG"></span>


在本部分中的示例 ProcAmp 函数演示如何实现 ProcAmp 控件功能。 这些示例函数将映射到[动作补偿回调函数](motion-compensation-callbacks.md)中定义[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。 您可以实现每个示例函数，以及如何将运动补偿代码模板以完成实现。 有关详细信息，请参阅[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

### <a name="span-iddeinterlacecontainerdeviceclasssamplefunctionsspanspan-iddeinterlacecontainerdeviceclasssamplefunctionsspanspan-iddeinterlacecontainerdeviceclasssamplefunctionsspandeinterlace-container-device-class-sample-functions"></a><span id="Deinterlace_Container_Device_Class_Sample_Functions"></span><span id="deinterlace_container_device_class_sample_functions"></span><span id="DEINTERLACE_CONTAINER_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>取消隔行扫描容器设备类示例函数

下表中的示例 ProcAmp 控制函数是成员函数*DXVA\_DeinterlaceContainerDeviceClass* （也就是说，它们使用调用取消隔行扫描容器设备）。 有关详细信息，请参阅[定义取消隔行扫描设备容器类](defining-the-deinterlace-container-device-class.md)并[执行 ProcAmp 控制和去隔行操作](performing-procamp-control-and-deinterlacing-operations.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps)"><strong>ProcAmpControlQueryCaps</strong></a></p></td>
<td align="left"><p>查询驱动程序以确定 ProcAmp 控制设备的输入的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryRange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange)"><strong>ProcAmpControlQueryRange</strong></a></p></td>
<td align="left"><p>查询驱动程序以确定最小值、 最大值、 步长和每个 ProcAmp 属性的默认值。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idprocampcontroldeviceclasssamplefunctionsspanspan-idprocampcontroldeviceclasssamplefunctionsspanspan-idprocampcontroldeviceclasssamplefunctionsspanprocamp-control-device-class-sample-functions"></a><span id="ProcAmp_Control_Device_Class_Sample_Functions"></span><span id="procamp_control_device_class_sample_functions"></span><span id="PROCAMP_CONTROL_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>ProcAmp 控制设备类示例函数

下表中的示例 ProcAmp 控制函数是成员函数*DXVA\_ProcAmpControlDeviceClass* （也就是说，它们称为使用 ProcAmp 控制设备）。 有关详细信息，请参阅[定义 ProcAmp 控制设备类](defining-the-procamp-control-device-class.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream" data-raw-source="[&lt;strong&gt;ProcAmpControlOpenStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream)"><strong>ProcAmpControlOpenStream</strong></a></p></td>
<td align="left"><p>创建一个 ProcAmp 流对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt" data-raw-source="[&lt;strong&gt;ProcAmpControlBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt)"><strong>ProcAmpControlBlt</strong></a></p></td>
<td align="left"><p>通过将输出写入到目标面执行 ProcAmp 调整操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream" data-raw-source="[&lt;strong&gt;ProcAmpControlCloseStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream)"><strong>ProcAmpControlCloseStream</strong></a></p></td>
<td align="left"><p>关闭 ProcAmp 流对象，并指示释放与该流关联的硬件资源的设备驱动程序。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanmapping-sample-functions-to-ddmotioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>示例函数映射到 DD\_MOTIONCOMPCALLBACKS

在本部分中的示例函数将映射到运动补偿回调函数，如下所示。 也就是说，每个示例函数调用中其各自的运动补偿回调。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps)"><strong>ProcAmpControlQueryCaps</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryRange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange)"><strong>ProcAmpControlQueryRange</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream" data-raw-source="[&lt;strong&gt;ProcAmpControlOpenStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream)"><strong>ProcAmpControlOpenStream</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt" data-raw-source="[&lt;strong&gt;ProcAmpControlBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt)"><strong>ProcAmpControlBlt</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream" data-raw-source="[&lt;strong&gt;ProcAmpControlCloseStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream)"><strong>ProcAmpControlCloseStream</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

 

 





