---
title: 反交错的示例函数
description: 反交错的示例函数
ms.assetid: a91c0267-7a3e-4206-8680-6e87778a329d
keywords:
- 取消隔行扫描 WDK DirectX va，因此示例函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 385cae818c80ccfbb938ce4e13f7ffaaf9091ed6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365614"
---
# <a name="sample-functions-for-deinterlacing"></a>反交错的示例函数


## <span id="ddk_sample_functions_for_deinterlacing_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_DEINTERLACING_GG"></span>


在本部分中的示例取消隔行扫描函数演示如何实现取消隔行和帧速率转换功能。 示例函数将映射到[动作补偿回调函数](motion-compensation-callbacks.md)中定义[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。 您可以实现每个示例函数，然后使用运动补偿代码模板以完成实现。 有关详细信息，请参阅[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

### <a name="span-iddeinterlacecontainerdeviceclasssamplefunctionsspanspan-iddeinterlacecontainerdeviceclasssamplefunctionsspanspan-iddeinterlacecontainerdeviceclasssamplefunctionsspandeinterlace-container-device-class-sample-functions"></a><span id="Deinterlace_Container_Device_Class_Sample_Functions"></span><span id="deinterlace_container_device_class_sample_functions"></span><span id="DEINTERLACE_CONTAINER_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>取消隔行扫描容器设备类示例函数

下表中的示例取消隔行扫描函数是成员函数*DXVA\_DeinterlaceContainerDeviceClass* （也就是说，它们通过调用取消隔行扫描容器设备）。 有关详细信息，请参阅[定义取消隔行扫描设备容器类](defining-the-deinterlace-container-device-class.md)并[执行 ProcAmp 控制和去隔行操作](performing-procamp-control-and-deinterlacing-operations.md)。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DeinterlaceQueryAvailableModes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes)"><strong>DeinterlaceQueryAvailableModes</strong></a></p></td>
<td align="left"><p>查询可用去隔行和帧速率转换模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DeinterlaceQueryModeCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)"><strong>DeinterlaceQueryModeCaps</strong></a></p></td>
<td align="left"><p>查询给定去隔行和帧速率转换模式的功能。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacebobdeviceclasssamplefunctionsspanspan-iddeinterlacebobdeviceclasssamplefunctionsspanspan-iddeinterlacebobdeviceclasssamplefunctionsspandeinterlace-bob-device-class-sample-functions"></a><span id="Deinterlace_Bob_Device_Class_Sample_Functions"></span><span id="deinterlace_bob_device_class_sample_functions"></span><span id="DEINTERLACE_BOB_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>取消隔行扫描 Bob 设备类示例函数

下表中的示例取消隔行扫描函数是成员函数*DXVA\_DeinterlaceBobDeviceClass* （也就是说，它们通过调用取消隔行扫描 bob 设备）。 有关详细信息，请参阅[定义取消隔行扫描 Bob 设备类](defining-the-deinterlace-bob-device-class.md)。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream" data-raw-source="[&lt;strong&gt;DeinterlaceOpenStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream)"><strong>DeinterlaceOpenStream</strong></a></p></td>
<td align="left"><p>打开视频流对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt" data-raw-source="[&lt;strong&gt;DeinterlaceBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)"><strong>DeinterlaceBlt</strong></a></p></td>
<td align="left"><p>提供了位块去隔行的视频流对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex" data-raw-source="[&lt;strong&gt;DeinterlaceBltEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)"><strong>DeinterlaceBltEx</strong></a></p></td>
<td align="left"><p><strong>Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本。</strong></p>
<div>
 
</div>
逐行视频和复合视频子流扫描上方的视频流。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream" data-raw-source="[&lt;strong&gt;DeinterlaceCloseStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream)"><strong>DeinterlaceCloseStream</strong></a></p></td>
<td align="left"><p>关闭视频流对象。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanmapping-sample-functions-to-ddmotioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>示例函数映射到 DD\_MOTIONCOMPCALLBACKS

下表中所示，在本部分中的示例函数将映射到运动补偿回调函数。 也就是说，每个示例函数调用中其各自的运动补偿回调。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DeinterlaceQueryAvailableModes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes)"><strong>DeinterlaceQueryAvailableModes</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DeinterlaceQueryModeCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)"><strong>DeinterlaceQueryModeCaps</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream" data-raw-source="[&lt;strong&gt;DeinterlaceOpenStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream)"><strong>DeinterlaceOpenStream</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt" data-raw-source="[&lt;strong&gt;DeinterlaceBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)"><strong>DeinterlaceBlt</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex" data-raw-source="[&lt;strong&gt;DeinterlaceBltEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)"><strong>DeinterlaceBltEx</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream" data-raw-source="[&lt;strong&gt;DeinterlaceCloseStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream)"><strong>DeinterlaceCloseStream</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

 

 





