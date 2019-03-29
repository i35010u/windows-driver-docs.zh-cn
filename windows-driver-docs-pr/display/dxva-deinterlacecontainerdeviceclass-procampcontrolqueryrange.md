---
title: ProcAmpControlQueryRange 方法
description: 示例 DXVA\_DeinterlaceContainerDeviceClass::ProcAmpControlQueryRange 函数允许 VMR 查询驱动程序以确定最小值、 最大值、 步长和每个 ProcAmp 属性的默认值。
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
ms.openlocfilehash: 88ab10bc4188c3df053b8f91b650a380311e864f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350221"
---
# <a name="dxvadeinterlacecontainerdeviceclassprocampcontrolqueryrange-method"></a>DXVA\_DeinterlaceContainerDeviceClass::ProcAmpControlQueryRange 方法


该示例**ProcAmpControlQueryRange**函数允许*VMR*要查询的驱动程序，以确定最小值、 最大值，请单步大小和每个 ProcAmp 属性的默认值。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlQueryRange(
  [in]  DWORD                   VideoProperty,
  [in]  DXVA_VideoDes           *lpVideoDescription,
  [out] DXVA_VideoPropertyRange *lpPropRange
);
```

<a name="parameters"></a>Parameters
----------

*VideoProperty* \[中\]标识驱动程序应为其返回信息的 ProcAmp 控件属性。 以下是此参数的可能值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXVA_ProcAmp_Brightness</p></td>
<td align="left"><p>返回亮度的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXVA_ProcAmp_Contrast</p></td>
<td align="left"><p>返回进行对比的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXVA_ProcAmp_Hue</p></td>
<td align="left"><p>返回 hue 的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXVA_ProcAmp_Saturation</p></td>
<td align="left"><p>返回饱和度的信息。</p></td>
</tr>
</tbody>
</table>

 

*lpVideoDescription* \[中\]提供一个指向[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)结构。 此结构可提供其描述为 ProcAmp 调整将应用于的视频驱动程序。 驱动程序可以调整它们 ProcAmp 对特定视频流支持。

*lpPropRange* \[出\]接收指向[ **DXVA\_VideoPropertyRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564083)结构，它指定范围、 步长、 和ProcAmp 的默认值。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码 (例如，电子\_NOTIMPL)。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

为每个 ProcAmp 属性 VMR 查询驱动程序以确定最小值、 最大值、 步长、 和默认值。 如果硬件不支持特定 ProcAmp 控件属性，则驱动程序应返回电子\_从 NOTIMPL **ProcAmpControlQueryRange**函数。

有关 ProcAmp 属性的详细信息，请参阅[ProcAmp 属性](https://msdn.microsoft.com/library/windows/hardware/ff569189)。

该示例**ProcAmpControlQueryRange**函数将映射到调用直接**RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。 **RenderMoComp**驱动程序提供指向成员[ **DdMoCompRender** ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调引用[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)结构。 DD\_RENDERMOCOMPDATA 结构填充，如下所示。

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
<td align="left"><p>dwNumBuffers</p></td>
<td align="left"><p>为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo</p></td>
<td align="left"><p>NULL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>dwFunction</p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryRangeFnCode</strong>常量 (在中定义<em>dxva.h</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpInputData</p></td>
<td align="left"><p>指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff564032" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlQueryRange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564032)"> <strong>DXVA_ProcAmpControlQueryRange</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpOutputData</p></td>
<td align="left"><p>指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff564083" data-raw-source="[&lt;strong&gt;DXVA_VideoPropertyRange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564083)"> <strong>DXVA_VideoPropertyRange</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

请注意，将不显示驱动程序提供 BeginMoCompFrame 或 EndMoCompFrame 要调用的函数首先调用 RenderMoComp 函数。

**示例代码**

以下代码举例说明如何实现您*ProcAmpControlQueryRange*函数：

```cpp
HRESULT
DXVA_DeinterlaceContainerDeviceClass::ProcAmpControlQueryRange(
    DWORD VideoProperty,
    LPDXVA_VideoDesc lpVideoDesc,
    DXVA_VideoPropertyRange* lpPropRange
    )
{
    // only the YUY2 and YV12 formats can be operated on
    if (lpVideoDesc->d3dFormat != '2YUY' &amp;&amp;
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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">N/A (Declared 驱动程序所提供的标头文件中。)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA\_ProcAmpControlQueryRange**](https://msdn.microsoft.com/library/windows/hardware/ff564032)

[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

[**DXVA\_VideoPropertyRange**](https://msdn.microsoft.com/library/windows/hardware/ff564083)

 

 






