---
title: DeinterlaceQueryModeCaps 方法
description: 示例 DXVA\_DeinterlaceContainerDeviceClass：:D einterlaceQueryModeCaps 函数查询驱动程序，以确定特定的隔行扫描模式的输入功能以及该模式可能支持的任何其他视频处理。
ms.assetid: 49070e57-2a93-447e-98d5-b98cded78b9c
keywords:
- DeinterlaceQueryModeCaps 方法显示设备
- DeinterlaceQueryModeCaps 方法显示设备，DXVA_DeinterlaceContainerDeviceClass 接口
- DXVA_DeinterlaceContainerDeviceClass 接口显示设备，DeinterlaceQueryModeCaps 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.DeinterlaceQueryModeCaps
api_location:
- N/A
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: f7b3b2e06439e3628855432a43ce77747eb36f8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838965"
---
# <a name="dxva_deinterlacecontainerdeviceclassdeinterlacequerymodecaps-method"></a>DXVA\_DeinterlaceContainerDeviceClass：:D einterlaceQueryModeCaps 方法


示例**DeinterlaceQueryModeCaps**函数查询驱动程序，以确定特定的隔行扫描模式的输入功能以及该模式可能支持的任何其他视频处理。

<a name="syntax"></a>语法
------

```cpp
HRESULT DeinterlaceQueryModeCaps(
  [in]  LPGUID               pGuidDeinterlaceMode,
  [in]  LPDXVA_VideoDesc     lpVideoDescription,
  [out] DXVA_DeinterlaceCaps *lpDeinterlaceCaps
);
```

<a name="parameters"></a>参数
----------

\] 中的*pGuidDeinterlaceMode* \[提供了一个指向用于指定取消隔行扫描模式的 GUID 的指针。

\] 中的*lpVideoDescription* \[提供一个指向[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)结构的指针，该结构定义要 deinterlaced 或进行速率转换的视频类型。

*lpDeinterlaceCaps* \[Out\] 接收指向包含隔行扫描模式功能的[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的指针。

<a name="return-value"></a>返回值
------------

如果成功，则返回零（\_确定或 DD\_正常）;否则，将返回错误代码。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

在 VMR 确定了可用于特定视频格式的隔行扫描模式后， *VMR*将查询该驱动程序的功能。 驱动程序从对其[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)函数的调用返回可用模式。

**DeinterlaceQueryModeCaps**函数报告[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构中给定模式的功能。

将*lpVideoDescription*参数传递给驱动程序，以便驱动程序可以支持源视频的分辨率和格式。 例如，驱动程序可能能够对480i 的内容执行三字段自适应隔行扫描，但它可能只允许 bob 1080i 内容。 有关详细信息，请参阅[视频内容进行取消隔行扫描和帧速率转换](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)。

所有驱动程序都应该能够使用现有的*位块传输*硬件支持 bob 模式。

**将 RenderMoComp 映射到*DeinterlaceQueryModeCaps***

**DeinterlaceQueryModeCaps**函数直接映射到[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**RenderMoComp**成员的调用。 **RenderMoComp**成员指向显示驱动程序提供的函数，该函数引用[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。

在未首先调用显示驱动程序提供的**BeginMoCompFrame**或**EndMoCompFrame**函数的情况下调用**RenderMoComp**回调。

DD\_RENDERMOCOMPDATA 结构按如下方式填充。

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
<td align="left"><p>无.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_DeinterlaceQueryAvailableModesFnCode</strong>常量（在<em>DXVA</em>中定义）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceQueryModeCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequerymodecaps)"><strong>DXVA_DeinterlaceQueryModeCaps</strong></a>结构的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)"><strong>DXVA_DeinterlaceCaps</strong></a>结构的指针。</p></td>
</tr>
</tbody>
</table>

 

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">不适用（在驱动程序提供的标头文件中声明）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequerymodecaps)

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

 

 






