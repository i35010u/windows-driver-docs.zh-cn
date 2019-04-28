---
title: ProcAmpControlBlt 方法
description: 示例 DXVA\_ProcAmpControlDeviceClass::ProcAmpControlBlt 函数执行 ProcAmp 调整的操作，将输出写入到目标图面。
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
ms.openlocfilehash: 409e7b7075f43e116e7cb399ddf94c6b43f4c275
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341101"
---
# <a name="dxvaprocampcontroldeviceclassprocampcontrolblt-method"></a>DXVA\_ProcAmpControlDeviceClass::ProcAmpControlBlt 方法


该示例*ProcAmpControlBlt*函数执行 ProcAmp 调整的操作，将输出写入到目标图面。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlBlt(
  [in] LPDDSURFACE            lpDDSDstSurface,
  [in] LPDDSURFACE            lpDDSSrcSurface,
  [in] DXVA_ProcAmpControlBlt *ccBlt
);
```

<a name="parameters"></a>Parameters
----------

*lpDDSDstSurface* \[中\]提供一个指向目标图面。

*lpDDSSrcSurface* \[中\]提供一个指向源图面。

*ccBlt* \[中\]提供一个指向[ **DXVA\_ProcAmpControlBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff564015)结构，它指定 ProcAmp 调整数据输出到目标面。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

源和目标矩形所需的 subrectangle ProcAmp 调整或拉伸。 支持拉伸是可选的由报告**VideoProcessingCaps**的成员[ **DXVA\_ProcAmpControlCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff564019)结构。 对 subrectangles 的支持也是可选的。

目标面可以在屏幕外平面，D3D 呈现目标、 D3D 纹理或也是呈现器目标的 D3D 纹理。 始终将在本地的视频内存分配目标图面。 目标表面的像素格式将 DXVA 中指定\_ProcAmpControlCaps 结构，除非正在 ProcAmp 调整过程执行 YUV 到 RGB 颜色空间转换。 在这种情况下，目标图面上格式将为至少 8 位的精度为每个颜色组件的 RGB 格式。

该示例*ProcAmpControlBlt*函数将映射到调用直接**RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。 **RenderMoComp**驱动程序提供指向成员*DdMoCompRender*回调引用[ **DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)结构。 DD\_RENDERMOCOMPDATA 结构填充，如下所示。

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
<td align="left"><p>必须是 2 的值的缓冲区数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>指向数组的两个图面。 数组的第一个元素是目标表面数组的第二个元素是源图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlBltFnCode</strong>常量 (在中定义<em>dxva.h</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff564015" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564015)"> <strong>DXVA_ProcAmpControlBlt</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>NULL。</p></td>
</tr>
</tbody>
</table>

 

对于 ProcAmp 控件使用的 DirectX VA 设备，RenderMoComp 称为而不会调用显示驱动程序提供 BeginMoCompFrame 或 EndMoCompFrame 函数。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

[**DXVA\_ProcAmpControlCaps**](https://msdn.microsoft.com/library/windows/hardware/ff564019)

[**DXVA\_ProcAmpControlBlt**](https://msdn.microsoft.com/library/windows/hardware/ff564015)

[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)

 

 






