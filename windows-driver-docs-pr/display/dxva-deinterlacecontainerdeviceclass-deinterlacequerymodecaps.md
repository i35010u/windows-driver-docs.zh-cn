---
title: DeinterlaceQueryModeCaps 方法
description: 示例 DXVA\_DeinterlaceContainerDeviceClass::DeinterlaceQueryModeCaps 函数查询驱动程序来确定特定的输入的功能取消隔行扫描模式和可能支持的任何其他视频处理模式。
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
ms.openlocfilehash: 7989613be2fd5f26d3aafd7395aace43c0360b20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562050"
---
# <a name="dxvadeinterlacecontainerdeviceclassdeinterlacequerymodecaps-method"></a>DXVA\_DeinterlaceContainerDeviceClass::DeinterlaceQueryModeCaps 方法


该示例**DeinterlaceQueryModeCaps**函数将查询来确定特定的输入的功能取消隔行扫描模式和任何附加视频处理过程，该模式可能支持的驱动程序。

<a name="syntax"></a>语法
------

```cpp
HRESULT DeinterlaceQueryModeCaps(
  [in]  LPGUID               pGuidDeinterlaceMode,
  [in]  LPDXVA_VideoDesc     lpVideoDescription,
  [out] DXVA_DeinterlaceCaps *lpDeinterlaceCaps
);
```

<a name="parameters"></a>Parameters
----------

*pGuidDeinterlaceMode* \[中\]提供一个指向用于指定取消隔行扫描模式下的 GUID。

*lpVideoDescription* \[中\]提供一个指向[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)结构，它定义类型的视频，deinterlaced 或转换率。

*lpDeinterlaceCaps* \[出\]接收指向[ **DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)结构，其中包含的功能取消隔行扫描模式。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

通过查询该驱动程序*VMR*取消隔行扫描模式后 VMR 已决定取消隔行扫描模式可用于特定的视频格式的功能。 该驱动程序返回可用模式通过调用其[ **DeinterlaceQueryAvailableModes** ](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)函数。

**DeinterlaceQueryModeCaps**函数报告给定模式中的功能[ **DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)结构。

*LpVideoDescription*参数传递给驱动程序，以便该驱动程序可以支持解析和源视频的格式。 例如，驱动程序可能能够执行三个字段自适应取消隔行扫描的 480i 内容，但它可能仅能 bob 1080i 内容。 有关详细信息，请参阅[取消隔行扫描和帧速率转换视频内容](https://msdn.microsoft.com/library/windows/hardware/ff570502)。

所有驱动程序应该能够支持使用现有的 bob 模式*位块传输*硬件。

**映射到 RenderMoComp *DeinterlaceQueryModeCaps***

**DeinterlaceQueryModeCaps**函数将映射到调用直接**RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。 **RenderMoComp**成员将指向引用的显示驱动程序提供函数[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)结构。

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
<th align="left">值</th>
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
<td align="left"><p>指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff563956" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceQueryModeCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563956)"> <strong>DXVA_DeinterlaceQueryModeCaps</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff563939" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563939)"> <strong>DXVA_DeinterlaceCaps</strong> </a>结构。</p></td>
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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">N/A (Declared 驱动程序所提供的标头文件中)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_DeinterlaceQueryModeCaps**](https://msdn.microsoft.com/library/windows/hardware/ff563956)

[**DXVA\_DeinterlaceCaps**](https://msdn.microsoft.com/library/windows/hardware/ff563939)

[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

 

 






