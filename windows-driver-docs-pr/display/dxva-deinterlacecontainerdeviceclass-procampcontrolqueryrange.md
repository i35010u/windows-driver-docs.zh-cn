---
title: ProcAmpControlQueryRange 方法
description: 示例 DXVA\_DeinterlaceContainerDeviceClass：:P rocAmpControlQueryRange 函数允许 VMR 查询驱动程序，以确定每个 ProcAmp 属性的最小值、最大值、步长大小和默认值。
ms.assetid: 13fd5d4b-f753-4a2c-80e0-c9614d7ebd3d
keywords:
- ProcAmpControlQueryRange 方法显示设备
- ProcAmpControlQueryRange 方法显示设备，DXVA_DeinterlaceContainerDeviceClass 接口
- DXVA_DeinterlaceContainerDeviceClass 接口显示设备，ProcAmpControlQueryRange 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.ProcAmpControlQueryRange
api_location:
- N/A
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 592cec315545cd788d3d7687c1acd144edefbd7a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838963"
---
# <a name="dxva_deinterlacecontainerdeviceclassprocampcontrolqueryrange-method"></a>DXVA\_DeinterlaceContainerDeviceClass：:P rocAmpControlQueryRange 方法


示例**ProcAmpControlQueryRange**函数允许*VMR*查询驱动程序，以确定每个 ProcAmp 属性的最小值、最大值、步长大小和默认值。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlQueryRange(
  [in]  DWORD                   VideoProperty,
  [in]  DXVA_VideoDes           *lpVideoDescription,
  [out] DXVA_VideoPropertyRange *lpPropRange
);
```

<a name="parameters"></a>参数
----------

\] 中的*VideoProperty* \[标识驱动程序应为其返回信息的 ProcAmp 控件属性。 下面是此参数的可能值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXVA_ProcAmp_Brightness</p></td>
<td align="left"><p>返回亮度信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXVA_ProcAmp_Contrast</p></td>
<td align="left"><p>返回对比度信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXVA_ProcAmp_Hue</p></td>
<td align="left"><p>返回色相信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXVA_ProcAmp_Saturation</p></td>
<td align="left"><p>返回饱和度信息。</p></td>
</tr>
</tbody>
</table>

 

\] 中的*lpVideoDescription* \[提供指向[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)结构的指针。 此结构为驱动程序提供了 ProcAmp 调整将应用到的视频的说明。 驱动程序可以调整其 ProcAmp 对特定视频流的支持。

*lpPropRange* \[Out\] 接收指向[**DXVA\_VideoPropertyRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange)结构的指针，该结构指定 ProcAmp 的范围、步长大小和默认值。

<a name="return-value"></a>返回值
------------

如果成功，则返回零（\_确定或 DD\_正常）;否则，将返回错误代码（例如，E\_NOTIMPL）。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

对于每个 ProcAmp 属性，VMR 会查询驱动程序以确定最小值、最大值、步长大小和默认值。 如果硬件不支持特定的 ProcAmp 控件属性，则驱动程序应从**ProcAmpControlQueryRange**函数返回 E\_NOTIMPL。

有关 ProcAmp 属性的详细信息，请参阅[ProcAmp properties](https://docs.microsoft.com/windows-hardware/drivers/display/procamp-properties)。

示例**ProcAmpControlQueryRange**函数直接映射到[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**RenderMoComp**成员的调用。 **RenderMoComp**成员指向驱动程序提供的[**DdMoCompRender**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调，该回调引用[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。 DD\_RENDERMOCOMPDATA 结构按如下方式填充。

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
<td align="left"><p>dwNumBuffers</p></td>
<td align="left"><p>无.</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo</p></td>
<td align="left"><p>NULL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>dwFunction</p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryRangeFnCode</strong>常量（在<em>DXVA</em>中定义）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpInputData</p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolqueryrange" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlQueryRange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolqueryrange)"><strong>DXVA_ProcAmpControlQueryRange</strong></a>结构的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpOutputData</p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange" data-raw-source="[&lt;strong&gt;DXVA_VideoPropertyRange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange)"><strong>DXVA_VideoPropertyRange</strong></a>结构的指针。</p></td>
</tr>
</tbody>
</table>

 

请注意，在未首先调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数的情况下，将调用 RenderMoComp 函数。

**示例代码**

下面的代码提供了一个示例，说明如何实现*ProcAmpControlQueryRange*函数：

```cpp
HRESULT
DXVA_DeinterlaceContainerDeviceClass::ProcAmpControlQueryRange(
    DWORD VideoProperty,
    LPDXVA_VideoDesc lpVideoDesc,
    DXVA_VideoPropertyRange* lpPropRange
    )
{
    // only the YUY2 and YV12 formats can be operated on
    if (lpVideoDesc->d3dFormat != '2YUY' &&
        lpVideoDesc->d3dFormat != '21VY') {
        return E_INVALIDARG;
    }
    // the following are the recommended settings for each property
    switch (VideoProperty) {
    case DXVA_ProcAmp_Brightness:
        lpPropRange->MinValue = -100.F;
        lpPropRange->MaxValue = 100.F;
        lpPropRange->DefaultValue = 0.0F;
        lpPropRange->StepSize = 0.1F;
        break;
    case DXVA_ProcAmp_Contrast:
        lpPropRange->MinValue = 0.F;
        lpPropRange->MaxValue = 10.F;
        lpPropRange->DefaultValue = 1.0F;
        lpPropRange->StepSize = 0.01F;
        break;
    case DXVA_ProcAmp_Hue:
        lpPropRange->MinValue = -180.0F;
        lpPropRange->MaxValue =  180.0F;
        lpPropRange->DefaultValue = 0.0F;
        lpPropRange->StepSize = 0.1F;
        break;
    case DXVA_ProcAmp_Saturation:
        lpPropRange->MinValue = 0.F;
        lpPropRange->MaxValue = 10.F;
        lpPropRange->DefaultValue = 1.0F;
        lpPropRange->StepSize = 0.01F;
        break;
    }
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


[**DXVA\_ProcAmpControlQueryRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolqueryrange)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_VideoPropertyRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange)

 

 






