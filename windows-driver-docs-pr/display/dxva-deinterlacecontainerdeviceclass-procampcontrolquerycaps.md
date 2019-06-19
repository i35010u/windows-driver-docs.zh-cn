---
title: ProcAmpControlQueryCaps 方法
description: 示例 DXVA\_DeinterlaceContainerDeviceClass::ProcAmpControlQueryCaps 函数允许 VMR 查询来确定 ProcAmp 控制设备和可能的其他视频处理操作的输入的要求该驱动程序受支持。
ms.assetid: e89f9a01-e8b3-4311-ad3b-296021c9795e
keywords:
- ProcAmpControlQueryCaps 方法显示设备
- ProcAmpControlQueryCaps 方法显示设备，DXVA_DeinterlaceContainerDeviceClass 接口
- DXVA_DeinterlaceContainerDeviceClass 接口显示设备，ProcAmpControlQueryCaps 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.ProcAmpControlQueryCaps
api_location:
- N/A
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 084a17ca78566a290b3f21631fb1483926b54981
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161578"
---
# <a name="dxvadeinterlacecontainerdeviceclassprocampcontrolquerycaps-method"></a>DXVA\_DeinterlaceContainerDeviceClass::ProcAmpControlQueryCaps 方法


该示例*ProcAmpControlQueryCaps*函数允许*VMR*查询来确定 ProcAmp 控制设备和可能的其他视频处理操作的输入的要求该驱动程序受支持。 查询可以出现 ProcAmp 调整操作正在执行时间。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlQueryCaps(
  [in]  DXVA_VideoDesc          *lpVideoDescription,
  [out] DXVA_ProcAmpControlCaps *lpProcAmpCaps
);
```

<a name="parameters"></a>Parameters
----------

*lpVideoDescription* \[中\]提供一个指向[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)结构，它定义的 ProcAmp 控件参数要处理的视频。

*lpProcAmpCaps* \[出\]接收指向[ **DXVA\_ProcAmpControlCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff564019)结构，其中包含的驱动程序功能ProcAmp 控制操作。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

驱动程序报告其功能与中的 ProcAmp 控件模式的用户模式组件[ **DXVA\_ProcAmpControlCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff564019)指向结构*lpProcAmpCaps*.

该示例*ProcAmpControlQueryCaps*函数将映射到调用直接**RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。 **RenderMoComp**驱动程序提供指向函数*DdMoCompRender*回调引用[ **DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)结构。 DD\_RENDERMOCOMPDATA 结构填充，如下所示。

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
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryCapsFnCode</strong>常量 (在中定义<em>dxva.h</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向一个实心<a href="https://msdn.microsoft.com/library/windows/hardware/ff564070" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564070)"> <strong>DXVA_VideoDesc</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff564019" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564019)"> <strong>DXVA_ProcAmpControlCaps</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

请注意，将不显示驱动程序提供 BeginMoCompFrame 或 EndMoCompFrame 要调用的函数首先调用 RenderMoComp 函数。

**示例代码**

以下代码举例说明如何实现您*ProcAmpControlQueryCaps*函数：

```cpp
HRESULT
DXVA_DeinterlaceContainerDeviceClass::ProcAmpControlQueryCaps(
    LPDXVA_VideoDesc lpVideoDesc,
    LPDXVA_ProcAmpControlCaps lpProcAmpControlCaps
    )
{
    // only the YUY2 and YV12 formats can be operated on
    if (lpVideoDesc->d3dFormat != '2YUY' &&
        lpVideoDesc->d3dFormat != '21VY') {
        return E_INVALIDARG;
    }
    lpProcAmpControlCaps->InputPool = D3DPOOL_DEFAULT;
    lpProcAmpControlCaps->d3dOutputFormat = lpVideoDesc->d3dFormat;
    lpProcAmpControlCaps->ProcAmpControlProps =
        DXVA_ProcAmp_Brightness |
        DXVA_ProcAmp_Contrast |
        DXVA_ProcAmp_Hue |
        DXVA_ProcAmp_Saturation;
    lpProcAmpControlCaps->VideoProcessingCaps = DXVA_VideoProcess_None;
    return S_OK;
}
```

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
<td align="left">N/A (Declared 驱动程序所提供的标头文件中。)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

[**DXVA\_ProcAmpControlCaps**](https://msdn.microsoft.com/library/windows/hardware/ff564019)

[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)

 

 






