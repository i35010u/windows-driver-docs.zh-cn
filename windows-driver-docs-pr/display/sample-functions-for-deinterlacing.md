---
title: 反交错的示例函数
description: 反交错的示例函数
ms.assetid: a91c0267-7a3e-4206-8680-6e87778a329d
keywords:
- 取消隔行扫描 WDK DirectX VA，示例函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 033ee7984ef026c69cd08d38c5dffdf73d8128dc
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715126"
---
# <a name="sample-functions-for-deinterlacing"></a>反交错的示例函数


## <span id="ddk_sample_functions_for_deinterlacing_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_DEINTERLACING_GG"></span>


本部分中的示例取消隔行扫描函数说明了如何实现取消隔行扫描和帧速率转换功能。 示例函数映射到[**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构中定义的[运动补偿回调函数](motion-compensation-callbacks.md)。 您可以实现每个示例函数，然后使用 "运动补偿代码" 模板来完成实现。 有关详细信息，请参阅 [DIRECTX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

### <a name="span-iddeinterlace_container_device_class_sample_functionsspanspan-iddeinterlace_container_device_class_sample_functionsspanspan-iddeinterlace_container_device_class_sample_functionsspandeinterlace-container-device-class-sample-functions"></a><span id="Deinterlace_Container_Device_Class_Sample_Functions"></span><span id="deinterlace_container_device_class_sample_functions"></span><span id="DEINTERLACE_CONTAINER_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>隔行扫描容器设备类示例函数

下表中的示例取消隔行扫描函数是 *DXVA \_ DeinterlaceContainerDeviceClass* (的成员函数，也就是说，使用隔行扫描容器设备) 调用它们。 有关详细信息，请参阅 [定义隔行扫描容器设备类](defining-the-deinterlace-container-device-class.md) 和 [执行 ProcAmp Control 和取消隔行扫描操作](performing-procamp-control-and-deinterlacing-operations.md)。

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
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DeinterlaceQueryAvailableModes&lt;/strong&gt;](./dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)"><strong>DeinterlaceQueryAvailableModes</strong></a></p></td>
<td align="left"><p>查询可用的取消隔行扫描和帧速率转换模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DeinterlaceQueryModeCaps&lt;/strong&gt;](./dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)"><strong>DeinterlaceQueryModeCaps</strong></a></p></td>
<td align="left"><p>查询给定取消隔行扫描和帧速率转换模式的功能。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlace_bob_device_class_sample_functionsspanspan-iddeinterlace_bob_device_class_sample_functionsspanspan-iddeinterlace_bob_device_class_sample_functionsspandeinterlace-bob-device-class-sample-functions"></a><span id="Deinterlace_Bob_Device_Class_Sample_Functions"></span><span id="deinterlace_bob_device_class_sample_functions"></span><span id="DEINTERLACE_BOB_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>隔行扫描 Bob 设备类示例函数

下表中的示例取消隔行扫描函数是 *DXVA \_ DeinterlaceBobDeviceClass* (的成员函数，也就是说，使用隔行扫描 bob 设备) 调用它们。 有关详细信息，请参阅 [定义隔行扫描 Bob 设备类](defining-the-deinterlace-bob-device-class.md)。

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
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream" data-raw-source="[&lt;strong&gt;DeinterlaceOpenStream&lt;/strong&gt;](./dxva-deinterlacebobdeviceclass-deinterlaceopenstream.md)"><strong>DeinterlaceOpenStream</strong></a></p></td>
<td align="left"><p>打开视频流对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt" data-raw-source="[&lt;strong&gt;DeinterlaceBlt&lt;/strong&gt;](./dxva-deinterlacebobdeviceclass-deinterlaceblt.md)"><strong>DeinterlaceBlt</strong></a></p></td>
<td align="left"><p>提供视频流对象的位块取消隔行扫描。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex" data-raw-source="[&lt;strong&gt;DeinterlaceBltEx&lt;/strong&gt;](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md)"><strong>DeinterlaceBltEx</strong></a></p></td>
<td align="left"><p><strong>Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本。</strong></p>
<div>
 
</div>
视频流顶部 Deinterlaces 视频和合成视频 substreams。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream" data-raw-source="[&lt;strong&gt;DeinterlaceCloseStream&lt;/strong&gt;](./dxva-deinterlacebobdeviceclass-deinterlaceclosestream.md)"><strong>DeinterlaceCloseStream</strong></a></p></td>
<td align="left"><p>关闭视频流对象。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmapping_sample_functions_to_dd_motioncompcallbacksspanspan-idmapping_sample_functions_to_dd_motioncompcallbacksspanspan-idmapping_sample_functions_to_dd_motioncompcallbacksspanmapping-sample-functions-to-dd_motioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>将示例函数映射到 DD \_ MOTIONCOMPCALLBACKS

本节中的示例函数映射到运动补偿回调函数，如下表所示。 也就是说，每个示例函数在其各自的运动补偿回调中调用。

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
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DeinterlaceQueryAvailableModes&lt;/strong&gt;](./dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)"><strong>DeinterlaceQueryAvailableModes</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DeinterlaceQueryModeCaps&lt;/strong&gt;](./dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)"><strong>DeinterlaceQueryModeCaps</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream" data-raw-source="[&lt;strong&gt;DeinterlaceOpenStream&lt;/strong&gt;](./dxva-deinterlacebobdeviceclass-deinterlaceopenstream.md)"><strong>DeinterlaceOpenStream</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt" data-raw-source="[&lt;strong&gt;DeinterlaceBlt&lt;/strong&gt;](./dxva-deinterlacebobdeviceclass-deinterlaceblt.md)"><strong>DeinterlaceBlt</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex" data-raw-source="[&lt;strong&gt;DeinterlaceBltEx&lt;/strong&gt;](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md)"><strong>DeinterlaceBltEx</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream" data-raw-source="[&lt;strong&gt;DeinterlaceCloseStream&lt;/strong&gt;](./dxva-deinterlacebobdeviceclass-deinterlaceclosestream.md)"><strong>DeinterlaceCloseStream</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

