---
title: DXVA\_DeinterlaceBobDeviceClass DeinterlaceBltEx 方法
description: 示例 DeinterlaceBltEx 函数执行取消隔行扫描或帧速率转换结合了 deinterlaced 或转换与提供视频的视频帧速率 substreams，并将合并的输出写入到目标图面。
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
ms.openlocfilehash: b4c7db76944cf84823098a6bf8547609b2e43ffa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521018"
---
# <a name="dxvadeinterlacebobdeviceclassdeinterlacebltex-method"></a>DXVA\_DeinterlaceBobDeviceClass::DeinterlaceBltEx 方法


该示例**DeinterlaceBltEx**函数执行取消隔行扫描帧速率转换结合了 deinterlaced 或转换与提供视频的视频帧速率 substreams，并将合并的输出写入到目标图面。

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

<a name="parameters"></a>参数
----------

*rtTargetFrame* \[中\]提供输出帧中的一系列输入帧的位置。 如果执行纯去隔行，则目标时间应与其中一个一致**rtStart**时间或中点时间 (也就是说，(**rtStart**+**rtEnd**) / 2) 的示例，如中所定义的[ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)结构。

如果请求的帧速率转换，则*rtTargetFrame*时间可能不同于任一**rtStart**时间或中点时间的示例。

*lprcTargetRect* \[中\]提供一个指向[ **RECT** ](https://msdn.microsoft.com/library/windows/hardware/ff569234)介绍哪些的目标面中的位置的结构**DeinterlaceBltEx**必须编写。 驱动程序使用*lprcTargetRect*来确定要写入的像素为单位。 请注意输出图像仅限于在矩形内的像素*lprcTargetRect*。 也就是说，在该矩形内的每个像素*lprcTargetRect*必须写入，并在矩形外的像素为单位*lprcTargetRect*不能修改。

*BackgroundColor* \[中\]提供[ **DXVA\_AYUVsample2** ](https://msdn.microsoft.com/library/windows/hardware/ff563116)标识背景的颜色和不透明度级别结构在其所有视频流和子流组成。 有关 Microsoft Windows Server 2003 SP1 和 Windows XP SP2，不透明度级别不使用，并且应忽略由驱动程序。

*dwDestinationFormat* \[中\]提供的格式信息处的指针中指定的目标面*lpDDSDstSurface*。 对于 Windows Server 2003 SP1 和 Windows XP SP2，此参数设置为 0。

*dwDestinationFlags* \[中\]提供这些标志指示上一目标图面中的当前目标面中的更改的集合。 此参数是按位 OR，一个或多个中的标志[ **DXVA\_DestinationFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff563963)枚举类型。 可以使用这些标志来优化您的驱动程序代码。 换而言之，你的代码不需要执行当前目标图面上的操作，如果从以前的目标面未不发生任何更改。

*lpDDSDstSurface* \[中\]提供一个指向目标图面。 目标面是位于视频内存的屏幕外纯图面。 中指定目标表面的像素格式**d3dOutputFormat**的成员[ **DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)结构。 YUV 颜色空间中必须是像素格式。

*lpDDSrcSurfaces* \[中\]提供一个指向数组 DXVA\_VideoSample2 结构描述视频源的引用示例和示例所需的位块传输的子流.

*dwNumSurfaces* \[中\]提供的示例中许多*lpDDSrcSurfaces*数组。

*fAlpha* \[中\]提供驱动程序应该应用到输出目标图面上的图像的背景色、 视频流和视频的子流组合的平面透明度值。 对于 Windows Server 2003 SP1 和 Windows XP SP2，此值始终为 1.0F，指示总体映像是不透明和整体图像没有 alpha 值混合处理是必需。

<a name="return-value"></a>返回值
------------

返回 0 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

**DeinterlaceBltEx**函数执行取消隔行扫描或帧速率转换操作，并同时将提供视频的子流与 deinterlaced 相结合或转换视频帧速率。 **DeinterlaceBltEx**函数将输出写入到目标图面。 请注意， **DeinterlaceBltEx**可以调用使用渐进式视频样本，在其中用例驱动程序不应执行取消隔行扫描操作。 驱动程序应将视频与提供的视频子流相结合，并将每个流转换所示*lprcTargetRect*并*BackgroundColor*参数和**rcSrc**并**rcDst**的成员[ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)中传递的数组中的结构*pDDSrcSurfaces*参数。

如果需要多个引用流取消隔行扫描模式用于渐进式视频，多个帧即使这些帧不需要以生成输出仍发送到该驱动程序。 有关详细信息，请参阅示例 5 中的[输入缓冲区顺序](https://msdn.microsoft.com/library/windows/hardware/ff567695)。

为引用中传递的数组中的视频样本*pDDSrcSurfaces*参数， **rtStart**并**rtEnd** DXVA 成员\_有关示例的 VideoSample2 结构指示示例的临时位置。 有关在数组中，每个视频的子流示例**rtStart**并**rtEnd** DXVA 成员\_VideoSample2 结构的每个示例清除为 0。

仅视频子流使用 AI44、 IA44 和 AYUV *FOURCC*像素格式可以提供给该驱动程序。 有关详细信息，请参阅[提供视频子流和目标图面](https://msdn.microsoft.com/library/windows/hardware/ff569751)。

调色板视频子流像素格式，对于**调色板**的成员[ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)结构包含每个视频的子流数组，该驱动程序时应使用 16 个调色板条目合成子流示例。 对于 nonpalletized 像素格式，调色板条目清零，并且可以忽略。

**SampleFlags**的成员[ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)结构的每个输入的示例包含一系列指示中的更改的标志上面的示例中的当前示例。 标志反映对调色板、 颜色数据、 源矩形和示例的目标矩形的更改。 可以使用这些标志来优化您的驱动程序代码。 换而言之，你的代码不需要执行在当前示例帧上的操作，如果前一示例帧未不发生任何更改。

*DwNumSurfaces*参数指示中的元素数*lpDDSrcSurface*数组。 Video 引用示例是首次在数组中后, 跟在 Z 顺序中视频的子流。 有关详细信息，请参阅[输入缓冲区顺序](https://msdn.microsoft.com/library/windows/hardware/ff567695)。 视频驱动程序收到的子流数的范围可以介于 0 到 15。 当**DeinterlaceBltEx**是调用，该驱动程序通常会收到 0 或 1 子视频流。 但是，必须实现该驱动程序，以便它可以处理多个视频的子流。

**DeinterlaceBltEx**函数将映射到调用直接**RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。 **RenderMoComp**成员将指向引用的显示驱动程序提供函数[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)结构。 DD\_RENDERMOCOMPDATA 结构填充，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dwNumBuffers</strong></p></td>
<td align="left"><p>指示指向数组中的条目数<strong>lpBufferInfo</strong>。 此数字是 1 加上的源代码示例。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>指向数组<a href="https://msdn.microsoft.com/library/windows/hardware/ff549652" data-raw-source="[&lt;strong&gt;DDMOCOMPBUFFERINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549652)"> <strong>DDMOCOMPBUFFERINFO</strong> </a>结构，其中一个为每个输入引用源示例或子流示例，另一个用于目标示例。 目标示例是数组的第一个元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p>指示<strong>DXVA_DeinterlaceBltExFnCode</strong>中定义常量<em>dxva.h</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向一个实心<a href="https://msdn.microsoft.com/library/windows/hardware/ff563915" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceBltEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563915)"> <strong>DXVA_DeinterlaceBltEx</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>设置为<strong>NULL</strong>、 当前不使用。</p></td>
</tr>
</tbody>
</table>

 

对于 DirectX VA 设备用于去隔行，驱动程序提供的回调指向**RenderMoComp**而不会调用驱动程序所提供的显示名为**BeginMoCompFrame**或**EndMoCompFrame**函数。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>版本： Windows Server 2003 SP1 及更高版本和 Windows XP SP2 和更高版本。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA\_AYUVsample2**](https://msdn.microsoft.com/library/windows/hardware/ff563116)

[**DXVA\_DeinterlaceBltEx**](https://msdn.microsoft.com/library/windows/hardware/ff563915)

[**DXVA\_DeinterlaceCaps**](https://msdn.microsoft.com/library/windows/hardware/ff563939)

[**DXVA\_DestinationFlags**](https://msdn.microsoft.com/library/windows/hardware/ff563963)

[**DXVA\_VideoSample2**](https://msdn.microsoft.com/library/windows/hardware/ff564092)

[**DDMOCOMPBUFFERINFO**](https://msdn.microsoft.com/library/windows/hardware/ff549652)

[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)

 

 






