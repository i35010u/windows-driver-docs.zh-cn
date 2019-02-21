---
title: KSPROPERTY\_扩展\_单元\_信息
description: KSPROPERTY\_扩展\_单元\_属性检索的扩展单元描述符 guidExtensionCode、 bNumControls、 bNrInPins 和 baSourceID 成员的信息。
ms.assetid: a7a2f655-8df7-4260-883f-53d6f5a7c6f3
keywords:
- KSPROPERTY_EXTENSION_UNIT_INFO 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTENSION_UNIT_INFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06cdecfe40ea2386046e2900dd330cae69d2e977
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546442"
---
# <a name="kspropertyextensionunitinfo"></a>KSPROPERTY\_扩展\_单元\_信息


KSPROPERTY\_扩展\_单元\_属性检索的扩展单元描述符 guidExtensionCode、 bNumControls、 bNrInPins 和 baSourceID 成员的信息。

## <span id="ddk_ksproperty_extension_unit_info_ks"></span><span id="DDK_KSPROPERTY_EXTENSION_UNIT_INFO_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>筛选器节点</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566720" data-raw-source="[&lt;strong&gt;KSP_NODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566720)"><strong>KSP_NODE</strong></a></p></td>
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性是在 Windows Vista 及更高版本，并适用于 Microsoft DirectX 9.2 或更高版本的 SDK。

设备在启动期间，系统提供的 USB 视频类驱动程序 (*Usbvideo.sys*) 将缓存从设备的扩展单元描述符信息。 *Usbvideo.sys*则使用此缓存信息以响应 KSPROPERTY\_扩展\_单元\_信息。

因此，此属性返回的字段均与所提供的扩展单元描述符中的设备相同。 此类描述符的示例，请参阅[示例扩展单元描述符](https://msdn.microsoft.com/library/windows/hardware/ff568133)。

具体而言，KSPROPERTY\_扩展\_单元\_信息返回扩展单元从描述符后面加上数据字段，如以下表中所示的 GUID。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>bNumControls</p></td>
<td><p>此扩展单元中的控件数。</p></td>
</tr>
<tr class="even">
<td><p>bNrInPins</p></td>
<td><p>扩展单元中的输入插针的数。</p></td>
</tr>
<tr class="odd">
<td><p>baSourceID(n)</p></td>
<td><p>单元或终端到哪些 pin 标识符<em>n</em>单元连接此扩展。 这是一个硬件标识符和不 DirectShow 标识符。</p></td>
</tr>
</tbody>
</table>

 

下面的代码示例演示如何提交 KSPROPERTY\_扩展\_单元\_信息，来自完整示例中所示[示例扩展单元插件 DLL](https://msdn.microsoft.com/library/windows/hardware/ff568134):

```cpp
ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = KSPROPERTY_EXTENSION_UNIT_INFO;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET | 
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &amp;ExtensionProp,
        sizeof(ExtensionProp),
        NULL,
        0,
        &amp;ulBytesReturned);
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
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统和 Microsoft DirectX 9.2 的 SDK 或更高版本中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>
