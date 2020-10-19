---
title: DXVA \_ DeinterlaceBobDeviceClass DeinterlaceBltEx 方法
description: 示例 DeinterlaceBltEx 函数执行取消隔行转换或帧速率转换，将 deinterlaced 或帧速率转换视频与提供的视频 substreams 合并，并将合并输出写入目标图面。
ms.assetid: 12a0e467-54f8-4cca-8ec0-aa8d04480ab6
keywords:
- DeinterlaceBltEx 方法显示设备
- DeinterlaceBltEx 方法显示设备，DXVA_DeinterlaceBobDeviceClass 接口
- DXVA_DeinterlaceBobDeviceClass 接口显示设备，DeinterlaceBltEx 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceBltEx
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e05720885c55af370ef541d91b9add59b01ae8f1
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185207"
---
# <a name="dxva_deinterlacebobdeviceclassdeinterlacebltex-method"></a>DXVA_DeinterlaceBobDeviceClass：:D einterlaceBltEx 方法

示例 **DeinterlaceBltEx** 函数执行取消隔行转换或帧速率转换，将 deinterlaced 或帧速率转换视频与提供的视频 substreams 合并，并将合并输出写入目标图面。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
HRESULT DeinterlaceBltEx(
  [in] REFERENCE_TIME      rtTargetFrame,
  [in] LPRECT              lprcTargetRect,
  [in] DXVA_AYUVsample2    BackgroundColor,
  [in] DWORD               dwDestinationFormat,
  [in] DWORD               dwDestinationFlags,
  [in] LPDDSURFACE         lpDDSDstSurface,
  [in] LPDXVA_VideoSample2 lpDDSrcSurfaces,
  [in] DWORD               dwNumSurfaces,
  [in] FLOAT               fAlpha
);
```

<a name="parameters"></a>parameters
----------

*rtTargetFrame* \[在 \] 输入帧序列中提供输出帧的位置。 如果执行了纯取消隔行扫描，则目标时间应与某个**rtStart**的时间或中点时间一致 (也就是说， (**rtStart** + **rtEnd**) /2) 示例，如[**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构中所定义。

如果请求帧速率转换，则 *rtTargetFrame* 时间可能不同于样本的 **rtStart** 时间或中点时间。

*lprcTargetRect* \[在中，提供了一个指向 \] [**RECT**](/windows/win32/api/windef/ns-windef-rect) 结构的指针，该结构描述了 **DeinterlaceBltEx** 必须写入到的目标图面中的位置。 驱动程序使用 *lprcTargetRect* 来确定要写入的像素。 请注意，输出图像限制为位于 *lprcTargetRect*的矩形内的像素。 也就是说，必须将位于 *lprcTargetRect* 的矩形内的每个像素写入到中，而不能修改 *lprcTargetRect* 的矩形之外的像素。

*BackgroundColor* \[在中 \] ，提供 [**DXVA \_ AYUVsample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_ayuvsample2) 结构，该结构标识所有视频流和 substreams 构成的背景的颜色和不透明度级别。 对于 Microsoft Windows Server 2003 SP1 和 Windows XP SP2，不使用不透明度级别，驱动程序应忽略它。

*dwDestinationFormat* \[在 \] *lpDDSDstSurface*的指针中指定的目标表面的 "提供格式信息" 中。 对于 Windows Server 2003 SP1 和 Windows XP SP2，此参数设置为0。

*dwDestinationFlags* \[在中 \] ，提供了一个标志集合，这些标志指示当前目标表面与前一个目标图面的变化。 此参数是 [**DXVA \_ DestinationFlags**](/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_destinationflags) 枚举类型中的一个或多个标志的按位 "或"。 可以使用这些标志优化驱动程序代码。 换言之，如果之前的目标表面没有发生任何更改，则代码不需要在当前目标表面上执行操作。

*lpDDSDstSurface* \[在中， \] 提供指向目标图面的指针。 目标图面是位于视频内存中的屏幕外无格式表面。 目标图面的像素格式是在[**DXVA \_ DeinterlaceCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的**d3dOutputFormat**成员中指定的。 像素格式必须在 YUV 颜色空间中。

*lpDDSrcSurfaces* \[在中， \] 提供指向 DXVA VideoSample2 结构的数组的指针 \_ ，这些结构描述了位块传输所需的视频源引用示例和子流示例。

*dwNumSurfaces* \[在中， \] 提供 *lpDDSrcSurfaces* 数组中的样本数。

*fAlpha* \[在中， \] 提供了驱动程序应应用于输出目标表面图像（这是背景色、视频流和视频 substreams）的平面透明度值。 对于 Windows Server 2003 SP1 和 Windows XP SP2，此值始终为 1.0 F，这表示总体图像是不透明的，并且不需要整体图像上的 alpha 混合。

<a name="return-value"></a>返回值
------------

如果成功，则返回 0 (S \_ \_) ; 否则返回 DD ok; 否则返回错误代码。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

**DeinterlaceBltEx**函数执行取消隔行转换或帧速率转换操作，同时将提供的视频 substreams 与 deinterlaced 或帧速率转换视频组合在一起。 然后， **DeinterlaceBltEx** 函数将输出写入目标图面。 请注意，可以使用渐进式视频示例调用 **DeinterlaceBltEx** ，在这种情况下，驱动程序不应执行隔行扫描操作。 驱动程序应将视频与提供的视频 substreams 相结合，并将每个流转换*为 lprcTargetRect*和*BackgroundColor*参数所指示的每个流，以及在*rcDst*参数中传递的数组中[**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的**rcSrc**和**pDDSrcSurfaces**成员。

如果将需要多个引用流的隔行扫描模式与渐进式视频一起使用，则即使这些帧不是生成输出所必需的，也仍会将多个帧发送到驱动程序。 有关详细信息，请参阅 [输入缓冲区顺序](./input-buffer-order.md)的示例5。

对于在 *pDDSrcSurfaces* 参数中传递的数组中的引用视频示例，示例的 DXVA VideoSample2 结构的 **rtStart** 和 **rtEnd** 成员 \_ 指示示例的临时位置。 对于数组中的每个视频子流示例，每个示例的 DXVA VideoSample2 结构的 **rtStart** 和 **rtEnd** 成员将 \_ 清除为0。

只有具有 AI44、IA44 和 AYUV *FOURCC* 像素格式的视频 substreams 可以提供给驱动程序。 有关详细信息，请参阅 [提供视频子流和目标面](./supplying-video-substream-and-destination-surfaces.md)。

对于托盘化视频子流像素格式，每个视频子流的[**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的**调色板**成员包含16个调色板项的数组，当组合子流示例时，驱动程序应使用这些项。 对于 nonpalletized 像素格式，会将调色板项清除为零，并可将其忽略。

每个输入示例的[**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的**SampleFlags**成员包含一系列标志，这些标志指示了上一示例中当前示例中的更改。 标志反映了对该示例的调色板、颜色数据、源矩形和目标矩形所做的更改。 可以使用这些标志优化驱动程序代码。 换句话说，如果上一个示例框架中没有发生任何更改，则代码不需要在当前示例帧上执行操作。

*DwNumSurfaces*参数指示*lpDDSrcSurface*数组中的元素数。 视频参考示例首先位于数组中，后面是以 Z 顺序显示的视频 substreams。 有关详细信息，请参阅 [输入缓冲区顺序](./input-buffer-order.md)。 驱动程序接收的视频 substreams 数的范围为0到15。 调用 **DeinterlaceBltEx** 时，驱动程序通常会收到0个或1个视频 substreams。 但是，必须实现该驱动程序，以便它可以处理多个视频 substreams。

**DeinterlaceBltEx**函数直接映射到[**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**RenderMoComp**成员的调用。 **RenderMoComp**成员指向显示驱动程序提供的、引用[**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)结构的函数。 \_按如下所示填充 DD RENDERMOCOMPDATA 结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dwNumBuffers</strong></p></td>
<td align="left"><p>指示 <strong>lpBufferInfo</strong>所指向的数组中的条目数。 此数字为1加上源样本的数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>指向 <a href="/windows/win32/api/ddrawint/ns-ddrawint-ddmocompbufferinfo" data-raw-source="[&lt;strong&gt;DDMOCOMPBUFFERINFO&lt;/strong&gt;](/windows/win32/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)"><strong>DDMOCOMPBUFFERINFO</strong></a> 结构的数组，每个输入引用源示例或子流示例各有一个，一个用于目标示例。 目标示例是数组的第一个元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p>指示<em>DXVA</em>中定义的<strong>DXVA_DeinterlaceBltExFnCode</strong>常数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向已填充的 <a href="/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceBltEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)"><strong>DXVA_DeinterlaceBltEx</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>设置为 <strong>NULL</strong>，当前未使用。</p></td>
</tr>
</tbody>
</table>

 

对于用于取消隔行扫描的 DirectX VA 设备，将在不调用显示器驱动程序提供的**BeginMoCompFrame**或**EndMoCompFrame**函数的情况下调用由**RenderMoComp**指向的驱动程序提供的回调。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>版本：仅限 Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA \_ AYUVsample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_ayuvsample2)

[**DXVA \_ DeinterlaceBltEx**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)

[**DXVA \_ DeinterlaceCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA \_ DestinationFlags**](/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_destinationflags)

[**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)

[**DDMOCOMPBUFFERINFO**](/windows/win32/api/ddrawint/ns-ddrawint-ddmocompbufferinfo)

[**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)
