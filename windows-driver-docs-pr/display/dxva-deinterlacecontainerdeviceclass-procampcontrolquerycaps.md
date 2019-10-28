---
title: ProcAmpControlQueryCaps 方法
description: 示例 DXVA\_DeinterlaceContainerDeviceClass：:P rocAmpControlQueryCaps 函数允许 VMR 查询驱动程序以确定 ProcAmp 控制设备的输入要求以及可能支持的其他视频处理操作.
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
ms.openlocfilehash: 9daafd95a48c6f312b6871ad90749075a14840c8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839715"
---
# <a name="dxva_deinterlacecontainerdeviceclassprocampcontrolquerycaps-method"></a>DXVA\_DeinterlaceContainerDeviceClass：:P rocAmpControlQueryCaps 方法


示例*ProcAmpControlQueryCaps*函数允许*VMR*查询驱动程序，以确定 ProcAmp 控制设备的输入要求以及可能支持的其他视频处理操作。 查询可以在执行 ProcAmp 调整操作的同时进行。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlQueryCaps(
  [in]  DXVA_VideoDesc          *lpVideoDescription,
  [out] DXVA_ProcAmpControlCaps *lpProcAmpCaps
);
```

<a name="parameters"></a>参数
----------

\] 中的*lpVideoDescription* \[提供一个指向[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)结构的指针，该结构定义要处理的视频的 ProcAmp 控件参数。

*lpProcAmpCaps* \[Out\] 接收指向[**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)结构的指针，该结构包含 ProcAmp 控件操作的驱动程序功能。

<a name="return-value"></a>返回值
------------

如果成功，则返回零（\_确定或 DD\_正常）;否则，将返回错误代码。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

驱动程序将其功能报告给 ProcAmp 控件模式的用户模式组件，该组件位于*lpProcAmpCaps*指向的[**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)结构中。

示例*ProcAmpControlQueryCaps*函数直接映射到[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**RenderMoComp**成员的调用。 **RenderMoComp**函数指向驱动程序提供的*DdMoCompRender*回调，该回调引用[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。 DD\_RENDERMOCOMPDATA 结构按如下方式填充。

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
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryCapsFnCode</strong>常量（在<em>DXVA</em>中定义）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向已填充的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)"><strong>DXVA_VideoDesc</strong></a>结构的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)"><strong>DXVA_ProcAmpControlCaps</strong></a>结构的指针。</p></td>
</tr>
</tbody>
</table>

 

请注意，在未首先调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数的情况下，将调用 RenderMoComp 函数。

**示例代码**

下面的代码提供了一个示例，说明如何实现*ProcAmpControlQueryCaps*函数：

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">不适用（在驱动程序提供的标头文件中声明）。</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)

[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

 

 






