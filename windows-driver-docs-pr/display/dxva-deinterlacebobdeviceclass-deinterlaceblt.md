---
title: DXVA \_ DeinterlaceBobDeviceClass DeinterlaceBlt 方法
description: 示例 DeinterlaceBlt 函数通过将输出写入目标图面来执行取消隔行转换或帧速率转换。
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
ms.openlocfilehash: 3f136eb65519f75f90ef60e19bc9d565c0d981fd
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064298"
---
# <a name="dxva_deinterlacebobdeviceclassdeinterlaceblt-method"></a>DXVA \_ DeinterlaceBobDeviceClass：:D einterlaceblt 方法


示例 *DeinterlaceBlt* 函数通过将输出写入目标图面来执行取消隔行转换或帧速率转换。

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

<a name="parameters"></a>parameters
----------

*rtTargetFrame* \[中的 \] 标识输入帧序列内的输出帧的位置。 如果只执行了取消隔行扫描，则目标时间应与参考样本的开始显示时间一致，如 [**DXVA \_ VideoSample**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample) 结构中所定义，或开始显示时间与结束显示时间之间的中点。 有关详细信息，请参阅 [**DXVA \_ DeinterlaceBlt**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt) 结构。

如果请求帧速率转换，则 **rtTarget** 时间可能不同于引用样本的任何 **rtStart** 时间。

*lprcDstRect* \[在中， \] 提供一个指向 [**RECT**](/windows/desktop/api/windef/ns-windef-tagrect) 结构的指针，该结构描述目标图面上矩形的左上角和右下角。 这些点定义应在其中发生位块传输的区域及其在目标图面上的位置。

*lpDDSDstSurface* \[在中， \] 提供指向目标图面的指针。 目标图面可以是 D3D 渲染器目标、D3D 纹理或同时也是渲染器目标的 D3D 纹理。 目标图面始终在本地视频内存中分配。

除非作为隔行扫描过程的一部分执行了 YUV 到 RGB 颜色空间转换，否则目标图面的像素格式为 [**DXVA \_ DeinterlaceCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps) 结构中所指示的格式。 在这种情况下，目标表面格式是 RGB 格式，每个颜色组件的精度至少为8位。

*lprcSrcRect* \[在中，提供了一个指向 \] RECT 结构的指针，该结构描述源图面上矩形的左上角和右下角。 这些点为位块传输定义源数据的区域及其在源图面上的位置。

*lpDDSrcSurfaces* \[在中 \] ，提供指向视频源示例的数组的指针。

*dwNumSurfaces* \[中的 \] 指示 **lpDDSrcSurfaces** 数组中的表面数。

*fAlpha* \[中的 \] 指示图面的 alpha 值。 值 0.0 F 指示透明图面。 值1.0 表示不透明。

<a name="return-value"></a>返回值
------------

如果成功，则返回零 (S \_ 正常或 DD \_ 确定) ; 否则返回错误代码。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

*DeinterlaceBlt*函数直接映射到[**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**RenderMoComp**成员的调用。 **RenderMoComp**成员指向显示驱动程序提供的、引用[**DD \_ RENDERMOCOMPDATA**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的函数。 \_按如下所示填充 DD RENDERMOCOMPDATA 结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dwNumBuffers</strong></p></td>
<td align="left"><p>指示 <strong>lpBufferInfo</strong>所指向的数组中的条目数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>指向 <a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo" data-raw-source="[&lt;strong&gt;DDMOCOMPBUFFERINFO&lt;/strong&gt;](/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)"><strong>DDMOCOMPBUFFERINFO</strong></a> 结构的数组，每个输入引用示例一个数组，另一个用于目标示例。 目标示例是数组的第一个元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p>指示<em>DXVA</em>中定义的<strong>DXVA_DeinterlaceBltFnCode</strong>常数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向已填充的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceBlt&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)"><strong>DXVA_DeinterlaceBlt</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>设置为 <strong>NULL</strong>，当前未使用。</p></td>
</tr>
</tbody>
</table>

 

对于用于取消隔行扫描的 DirectX VA 设备，将在不调用显示器驱动程序提供的**BeginMoCompFrame**或**EndMoCompFrame**函数的情况下调用由**RenderMoComp**指向的驱动程序提供的回调。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD \_ RENDERMOCOMPDATA**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DXVA \_ DeinterlaceBlt**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)

[**DXVA \_ DeinterlaceCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA \_ VideoSample**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample)

 

