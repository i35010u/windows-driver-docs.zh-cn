---
title: DeinterlaceQueryAvailableModes 方法
description: 示例 DXVA\_DeinterlaceContainerDeviceClass::DeinterlaceQueryAvailableModes 函数查询针对特定的输入视频格式的可用去隔行或帧速率转换模式。
ms.assetid: be721bde-3c72-4942-9f33-5ea1bf2d187c
keywords:
- DeinterlaceQueryAvailableModes 方法显示设备
- DeinterlaceQueryAvailableModes 方法显示设备，DXVA_DeinterlaceContainerDeviceClass 接口
- DXVA_DeinterlaceContainerDeviceClass 接口显示设备，DeinterlaceQueryAvailableModes 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.DeinterlaceQueryAvailableModes
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: d2f3195b3fbc9b73786a2a4c8f7fa5fd7f2b3442
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375833"
---
# <a name="dxvadeinterlacecontainerdeviceclassdeinterlacequeryavailablemodes-method"></a>DXVA\_DeinterlaceContainerDeviceClass::DeinterlaceQueryAvailableModes 方法


该示例*DeinterlaceQueryAvailableModes*函数针对特定的输入视频格式的可用去隔行或帧速率转换模式的查询。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
HRESULT DeinterlaceQueryAvailableModes(
  [in]      LPDXVA_VideoDesc lpVideoDescription,
  [in, out] LPDWORD          lpdwNumModesSupported,
  [in, out] LPGUID           pGuidsDeinterlaceModes
);
```

<a name="parameters"></a>Parameters
----------

*lpVideoDescription* \[中\]提供一个指向[ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)结构，其中包含的视频流的说明若要执行去隔行或帧速率转换。

*lpdwNumModesSupported* \[传入、 传出\]接收到取消隔行扫描或帧速率转换模式，在数组中返回数的指针*pGuidsDeinterlaceModes*。

*pGuidsDeinterlaceModes* \[in、 out\]接收指向表示驱动程序支持的取消隔行扫描或帧速率转换模式的 Guid 的数组。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

*LpVideoDescription*参数传递给驱动程序，以便该驱动程序可以支持解析和源视频的格式。 例如，驱动程序可能能够执行三个字段自适应取消隔行扫描的 480i 内容，但它可能仅能 bob 1080i 内容。 有关详细信息，请参阅[取消隔行扫描和帧速率转换视频内容](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)。

返回的 Guid *pGuidsDeinterlaceModes*应按顺序的降序质量返回参数 （即，最高的质量模式应占用返回的 GUID 数组的第一个元素）。

所有驱动程序应该能够支持使用现有的 bob 模式*位块传输*(blt) 硬件。 有关模式的详细信息，请参阅[取消隔行扫描模式](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-modes)并[帧速率转换模式](https://docs.microsoft.com/windows-hardware/drivers/display/frame-rate-conversion-modes)主题。

驱动程序将返回它从请求响应中支持的 Guid （模式） *VMR*。 该驱动程序响应调用其[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 驱动程序将返回通过 Guid **lpOutputData**的成员[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构到*lpRenderData*的参数*DdMoCompRender*点。 **LpOutputData**成员将指向[ **DXVA\_DeinterlaceQueryAvailableModes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)结构，其中包含的 Guid 数组中**Guid**成员。

**映射到 RenderMoComp** ***DeinterlaceQueryAvailableModes***

该示例*DeinterlaceQueryAvailableModes*函数将映射到调用直接**RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。 **RenderMoComp**成员将指向引用的显示驱动程序提供函数[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。

**RenderMoComp**驱动程序所提供的显示没有调用回调**BeginMoCompFrame**或**EndMoCompFrame**函数首先调用。

DD\_RENDERMOCOMPDATA 结构填充，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dwNumBuffers</strong></p></td>
<td align="left"><p>为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_DeinterlaceQueryAvailableModesFnCode</strong>常量 (在中定义<em>dxva.h</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向一个实心<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)"> <strong>DXVA_VideoDesc</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceQueryAvailableModes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)"> <strong>DXVA_DeinterlaceQueryAvailableModes</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

之后*VMR*已决定取消隔行扫描或帧转换模式适用于特定的视频格式，VMR 查询驱动程序以获取有关特定取消隔行扫描模式下的输入要求的详细的信息和任何附加视频处理过程，该模式可能支持。 驱动程序将返回此信息通过调用其[ **DeinterlaceQueryModeCaps** ](dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)函数。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DeinterlaceQueryModeCaps**](dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_SampleFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_sampleformat)

 

 






