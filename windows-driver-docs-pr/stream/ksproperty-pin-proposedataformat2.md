---
title: KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2
description: 操作系统将使用 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2 属性来确定是否 pin 工厂实例化 pin 支持特定的数据格式。
ms.assetid: 64F6E8CA-8E48-43B3-9A60-DAB53516AD45
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT2 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT2
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 12/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1a9148b21b1d9c5c3c49dcbd9de9a2e353371e4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534794"
---
# <a name="kspropertypinproposedataformat2"></a>KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2


OS 使用**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**属性以确定驱动程序是否具有给定指定的属性对 pin 的首选的数据格式。

## <a name="usage-summary-table"></a>使用率摘要表


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
<td><p>Filter</p></td>
<td><p>请参阅备注</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

属性描述符[ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)跟[ **KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)指定大小可变的计数属性后面**KSMULTIPLE\_项**。 每个属性开头[ **KSATTRIBUTE** ](https://msdn.microsoft.com/library/windows/hardware/ff560987)标头后跟特定数据到该属性。 属性充当属性请求，指定建议的数据格式的参数。

**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**包含类型的结构[ **KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff561656)，

对该属性是受支持的唯一属性*KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_模式*且使用指定[ **KSATTRIBUTE\_AUDIOSIGNALPROCESSING\_模式下**](https://msdn.microsoft.com/library/windows/hardware/mt727947)结构。 请注意， **KSATTRIBUTE\_AUDIOSIGNALPROCESSING\_模式**结构开头[ **KSATTRIBUTE** ](https://msdn.microsoft.com/library/windows/hardware/ff560987)成员。 有关详细信息，请参阅[音频信号处理模式](https://msdn.microsoft.com/library/windows/hardware/mt186386)。

[**KSPROPERTY\_类型\_获取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)当 pin 已建议格式时才支持。 此函数允许音频驱动程序给出指定的属性对 pin 提供的默认数据格式有关的信息。

KS 筛选器返回 STATUS_SUCCESS pin 是否为指定的特性的首选的数据格式。 如果 pin 不具有指定属性的首选的数据格式将其返回 STATUS_NOT_SUPPORTED。 对于任何其他失败，返回相应的错误。 如果驱动程序支持此属性，OS 将始终为特定信号处理模式下使用此格式。 KSPROPERTY_TYPE_SET 不支持此属性。

**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2 输入结构**

下表介绍 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2 输入结构*PinProperty*元素。

|                            |                                                                                                                                                                                    |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PinProperty.Property.Set   | PinProperty.Property.Set 应设置为[KSPROPSETID\_Pin](kspropsetid-pin.md)为请求的模式。                                                                  |
| PinProperty.Property.Id    | PinProperty.Property.Id 始终设置为**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**。                                                                                              |
| PinProperty.Property.Flags | PinProperty.Property.Flags 可以设置为[ **KSPROPERTY\_类型\_获取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)或 KSPROPERTY\_类型\_BASICSUPPORT，若要了解基本有关属性的信息。 |
| PinProperty.PinId          | PinProperty.PinId 标识的目标 pin **KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**请求。                                                                           |
| PinProperty.Reserved       | PinProperty.Reserved 是保留供将来使用，应始终设置为零 (0)。                                                                                          |

 

下表介绍 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2 输入结构*属性*元素。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Attributes.Count</td>
<td>Attributes.Count 应设置为属性，通常一 (1) 的数目。</td>
</tr>
<tr class="even">
<td>Attributes.Size</td>
<td>Attributes.Size 应设置为 ProposeDataformat2Input 的大小。 它可以像这样，当一个属性时计算：
<p>sizeof(ProposeDataformat2Input)</p></td>
</tr>
</tbody>
</table>

 

下表介绍 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2 输入结构*SignalProcessingModeAttribute*元素。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>SignalProcessingModeAttribute.AttributeHeader.Attribute</td>
<td>AttributeHeader.Attribute 元素应设置为所需 KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE。</td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute.AttributeHeader.Flags</td>
<td>标志元素保留供将来使用，并且应始终设置为零 (0)。</td>
</tr>
<tr class="odd">
<td>SignalProcessingModeAttribute.AttributeHeader.Size</td>
<td>AttributeHeader.Size 指示的大小<a href="https://msdn.microsoft.com/library/windows/hardware/mt727947" data-raw-source="[&lt;strong&gt;KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt727947)"> <strong>KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE</strong></a>。 它可以计算如下：
<p>sizeof(KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE)</p></td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute.SignalProcessingMode</td>
<td>SignalProcessingMode 元素应设置为请求 SIGNALPROCESSINGMODE 等 AUDIO_SIGNALPROCESSINGMODE_DEFAULT。</td>
</tr>
</tbody>
</table>

 

若要使用**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**定义以下结构。

```cpp
typedef struct
{
    KSP_PIN                                 PinProperty;
    KSMULTIPLE_ITEM                         Attributes;
    KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE  SignalProcessingModeAttribute;
} ProposeDataformat2Input;
```

此代码示例演示如何初始化结构。

```cpp
    ProposeDataformat2Input input = {0};

    input.PinProperty.Property.Set = KSPROPSETID_Pin;  
    input.PinProperty.Property.Id = KSPROPERTY_PIN_PROPOSEDATAFORMAT2;  
    input.PinProperty.Property.Flags = KSPROPERTY_TYPE_GET;  
    input.PinProperty.PinId = m_nPinId;  
    input.PinProperty.Reserved = 0;     

    input.Attributes.Count = 1;
    input.Attributes.Size = sizeof(ProposeDataformat2Input) - RTL_SIZEOF_THROUGH_FIELD(ProposeDataformat2Input, PinProperty);

    input.SignalProcessingModeAttribute.AttributeHeader.Attribute = KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE;
    input.SignalProcessingModeAttribute.AttributeHeader.Flags = 0;
    input.SignalProcessingModeAttribute.AttributeHeader.Size = sizeof(KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE);
    input.SignalProcessingModeAttribute.SignalProcessingMode = gProcessingMode;
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
<td><p>从开始提供 Windows 8.1。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSDATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff561656)

 

 






