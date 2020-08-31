---
title: ProcAmpControlBlt 方法
description: 示例 DXVA \_ ProcAmpControlDeviceClass：:P rocampcontrolblt 函数通过将输出写入目标图面来执行 ProcAmp 调整操作。
ms.assetid: bf86fd39-554d-4ef1-adb7-202bb70fd3b4
keywords:
- ProcAmpControlBlt 方法显示设备
- ProcAmpControlBlt 方法显示设备，DXVA_ProcAmpControlDeviceClass 接口
- DXVA_ProcAmpControlDeviceClass 接口显示设备，ProcAmpControlBlt 方法
topic_type:
- apiref
api_name:
- DXVA_ProcAmpControlDeviceClass.ProcAmpControlBlt
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 91c21e70d412e8ece5435eea6358ad4de256ed88
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063108"
---
# <a name="dxva_procampcontroldeviceclassprocampcontrolblt-method"></a>DXVA \_ ProcAmpControlDeviceClass：:P rocampcontrolblt 方法


示例 *ProcAmpControlBlt* 函数通过将输出写入目标图面来执行 ProcAmp 调整操作。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlBlt(
  [in] LPDDSURFACE            lpDDSDstSurface,
  [in] LPDDSURFACE            lpDDSSrcSurface,
  [in] DXVA_ProcAmpControlBlt *ccBlt
);
```

<a name="parameters"></a>parameters
----------

*lpDDSDstSurface* \[在中， \] 提供指向目标图面的指针。

*lpDDSSrcSurface* \[在中， \] 提供指向源图面的指针。

*ccBlt* \[在中， \] 提供指向 [**DXVA \_ ProcAmpControlBlt**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt) 结构的指针，该结构指定 ProcAmp 调整数据输出到目标图面。

<a name="return-value"></a>返回值
------------

如果成功，则返回零 (S \_ 正常或 DD \_ 确定) ; 否则返回错误代码。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

源和目标矩形对于 subrectangle ProcAmp 调整或拉伸是必需的。 支持拉伸是可选的，由[**DXVA \_ ProcAmpControlCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)结构的**VideoProcessingCaps**成员报告。 对 subrectangles 的支持也是可选的。

目标图面可以是离线平面、D3D 渲染器目标、D3D 纹理或同时也是渲染器目标的 D3D 纹理。 目标图面将始终在本地视频内存中分配。 \_除非在 ProcAmp 调整过程中执行了 YUV 到 RGB 的颜色空间转换，否则目标图面的像素格式将为 DXVA ProcAmpControlCaps 结构中所指示的格式。 在这种情况下，目标表面格式将为 RGB 格式，每个颜色组件的精度至少为8位。

示例*ProcAmpControlBlt*函数直接映射到[**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**RenderMoComp**成员的调用。 **RenderMoComp**成员指向驱动程序提供的*DdMoCompRender*回调，该回调引用[**DD \_ RENDERMOCOMPDATA**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。 \_按如下所示填充 DD RENDERMOCOMPDATA 结构。

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
<td align="left"><p>缓冲区数，必须为值2。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>指向两个图面的数组的指针。 数组的第一个元素是目标图面;数组的第二个元素是源图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><em>DXVA</em>) 中定义<strong>DXVA_ProcAmpControlBltFnCode</strong>常量 (。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlBlt&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt)"><strong>DXVA_ProcAmpControlBlt</strong></a> 结构的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>NULL。</p></td>
</tr>
</tbody>
</table>

 

对于用于 ProcAmp 控制的 DirectX VA 设备，将调用 RenderMoComp，而不会调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA \_ ProcAmpControlCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)

[**DXVA \_ ProcAmpControlBlt**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt)

[**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD \_ CREATEMOCOMPDATA**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

 

