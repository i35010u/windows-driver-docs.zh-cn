---
title: DXVA\_DeinterlaceBobDeviceClass DeinterlaceBlt 方法
description: 示例 DeinterlaceBlt 函数执行取消隔行扫描的帧速率转换通过将输出写入到目标图面。
ms.assetid: 0aa68d0c-8c2b-41fe-9e46-a41b157fbd98
keywords:
- DeinterlaceBlt 方法显示设备
- DeinterlaceBlt 方法显示设备，DXVA_DeinterlaceBobDeviceClass 接口
- DXVA_DeinterlaceBobDeviceClass 接口显示设备，DeinterlaceBlt 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceBlt
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ba69f86e410be7b0358903eb8408a1e5d6441f5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375849"
---
# <a name="dxvadeinterlacebobdeviceclassdeinterlaceblt-method"></a>DXVA\_DeinterlaceBobDeviceClass::DeinterlaceBlt 方法


该示例*DeinterlaceBlt*函数执行取消隔行扫描或通过将输出写入到目标表面的帧速率转换。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
HRESULT DeinterlaceBlt(
  [in] REFERENCE_TIME     rtTargetFrame,
  [in] LPRECT             lprcDstRect,
  [in] LPDDSURFACE        lpDDSDstSurface,
  [in] LPRECT             lprcSrcRect,
  [in] LPDXVA_VideoSample lpDDSrcSurfaces,
  [in] DWORD              dwNumSurfaces,
  [in] FLOAT              fAlpha
);
```

<a name="parameters"></a>Parameters
----------

*rtTargetFrame* \[中\]标识输出帧中的一系列输入帧的位置。 如果仅执行去隔行，目标时间应保持一致使用引用的示例中，开始显示时间中定义[ **DXVA\_VideoSample** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample)结构，或开始显示时间和结束的显示时间之间的中点。 有关详细信息，请参阅[ **DXVA\_DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt)结构。

如果请求的帧速率转换，则**rtTarget**时间可能不同于任一**rtStart**引用示例中的时间。

*lprcDstRect* \[中\]提供一个指向[ **RECT** ](https://docs.microsoft.com/windows/desktop/api/windef/ns-windef-tagrect)结构，用于描述左上并降低正确的位置，在目标上的矩形的图面。 这些点定义中的区域，这位块传输应发生，其目标图面上的位置。

*lpDDSDstSurface* \[中\]提供一个指向目标图面。 目标面可以是 D3D 呈现目标、 D3D 纹理或也是呈现器目标的 D3D 纹理。 在本地的视频内存中始终分配目标图面。

目标表面的像素格式是所示[ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)结构，除非正在作为的一部分执行的 YUV 到 RGB 颜色空间转换取消隔行扫描过程。 在这种情况下，目标图面上格式为至少 8 位的精度为每个颜色组件的 RGB 格式。

*lprcSrcRect* \[中\]提供指向介绍左上并降低正确的位置的源图面上的一个矩形的 RECT 结构的指针。 这些点定义的源数据的区域，以便位块传送和源表面上的其位置。

*lpDDSrcSurfaces* \[中\]提供指向视频源示例的数组的指针。

*dwNumSurfaces* \[中\]指示的图面中**lpDDSrcSurfaces**数组。

*fAlpha* \[中\]指示表面的 alpha 值。 0\.0F 的值表示透明的图面。 1\.0 f 的值表示一个不透明的图面。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

*DeinterlaceBlt*函数将映射到调用直接**RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。 **RenderMoComp**成员将指向引用的显示驱动程序提供函数[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。 DD\_RENDERMOCOMPDATA 结构填充，如下所示。

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
<td align="left"><p>指示指向数组中的条目数<strong>lpBufferInfo</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>指向数组<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo" data-raw-source="[&lt;strong&gt;DDMOCOMPBUFFERINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)"> <strong>DDMOCOMPBUFFERINFO</strong> </a>结构，其中一个为每个输入引用示例，另一个用于目标示例。 目标示例是数组的第一个元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p>指示<strong>DXVA_DeinterlaceBltFnCode</strong>中定义常量<em>dxva.h</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向一个实心<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt)"> <strong>DXVA_DeinterlaceBlt</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>设置为<strong>NULL</strong>、 当前不使用。</p></td>
</tr>
</tbody>
</table>

 

对于 DirectX VA 设备用于去隔行，驱动程序提供的回调指向**RenderMoComp**而不会调用驱动程序所提供的显示名为**BeginMoCompFrame**或**EndMoCompFrame**函数。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DXVA\_DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt)

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA\_VideoSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample)

 

 






