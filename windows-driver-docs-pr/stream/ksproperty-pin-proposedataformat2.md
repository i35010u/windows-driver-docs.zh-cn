---
title: KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2
description: 操作系统使用 KSPROPERTY \_ 引脚 \_ PROPOSEDATAFORMAT2 属性来确定 pin 工厂实例化的 pin 是否支持特定的数据格式。
ms.assetid: 64F6E8CA-8E48-43B3-9A60-DAB53516AD45
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT2 流媒体设备
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
ms.openlocfilehash: c94b767a9ad49e3f57b3c51d774efbd47af6b553
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190887"
---
# <a name="ksproperty_pin_proposedataformat2"></a>KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2


操作系统使用 **KSPROPERTY \_ 引脚 \_ PROPOSEDATAFORMAT2** 属性来确定在给定指定属性的情况上驱动程序是否具有首选的数据格式。

## <a name="usage-summary-table"></a>使用情况摘要表


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
<th>获取</th>
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
<td><p>筛选器</p></td>
<td><p>请参阅 "备注"</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

属性描述符是一个 [**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) ，后跟一个 [**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item) ，它指定跟随 **KSMULTIPLE \_ 项**的可变大小属性的计数。 每个属性都以 [**KSATTRIBUTE**](/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute) 标头开头，后面是特定于该特性的数据。 属性作为属性请求的参数，指定建议的数据格式。

**KSPROPERTY \_PIN \_ PROPOSEDATAFORMAT2** 包含 [**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)类型的结构，

属性支持的唯一属性为 *KSATTRIBUTEID \_ AUDIOSIGNALPROCESSING \_ 模式* ，并且是使用 [**KSATTRIBUTE \_ AUDIOSIGNALPROCESSING \_ mode**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode) 结构指定的。 请注意， **KSATTRIBUTE \_ AUDIOSIGNALPROCESSING \_ 模式** 结构以 [**KSATTRIBUTE**](/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute) 成员开头。 有关详细信息，请参阅 [音频信号处理模式](../audio/audio-signal-processing-modes.md)。

[**KSPROPERTY \_仅 \_ **](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) 当 pin 具有建议格式时才支持类型 GET。 此函数允许音频驱动程序提供有关指定属性的 pin 的默认数据格式的信息。

如果 pin 对于指定的特性具有首选数据格式，则 KS 筛选器将返回 STATUS_SUCCESS。 如果 pin 对于指定的属性没有首选数据格式，它将返回 STATUS_NOT_SUPPORTED。 对于其他任何失败，将返回相应的错误。 如果驱动程序支持此属性，则 OS 始终将此格式用于特定的信号处理模式。 此属性不支持 KSPROPERTY_TYPE_SET。

**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2 输入结构**

下表提供了 KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2 Input structure *PinProperty* 元素的说明。

**PinProperty**：应将 PinProperty 设置为请求模式下的 [KSPROPSETID \_ 插针](kspropsetid-pin.md) 。

**PinProperty.Property.Id**： PinProperty.Property.Id 始终设置为 **KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2**。

**PinProperty**：可将 PinProperty 设置为 [**KSPROPERTY \_ 类型 \_ GET**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) 或 KSPROPERTY \_ type \_ BASICSUPPORT，以了解有关属性的基本信息。

**PinProperty. PinId**： PinProperty 标识 **KSPROPERTY \_ pin \_ PROPOSEDATAFORMAT2** 请求的目标 pin。

**PinProperty**：保留 PinProperty 供将来使用，并且应始终设置为零 (0) 。


 

下表提供了 KSPROPERTY \_ 引脚 \_ PROPOSEDATAFORMAT2 Input structure *属性* 元素的说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>特性. 计数</td>
<td>特性. Count 应设置为属性的数目，通常为一 (1) 。</td>
</tr>
<tr class="even">
<td>特性。大小</td>
<td>特性. 应将大小设置为 ProposeDataformat2Input 的大小。 如果有一个属性，则可按如下方式计算：
<p>sizeof (ProposeDataformat2Input) </p></td>
</tr>
</tbody>
</table>

 

下表提供了 KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2 Input structure *SignalProcessingModeAttribute* 元素的说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>SignalProcessingModeAttribute. AttributeHeader. 特性</td>
<td>应将 AttributeHeader 元素设置为所需 KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE。</td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute. AttributeHeader</td>
<td>Flags 元素保留供将来使用，并且应始终设置为零 (0) 。</td>
</tr>
<tr class="odd">
<td>SignalProcessingModeAttribute. AttributeHeader</td>
<td>AttributeHeader 指示 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode" data-raw-source="[&lt;strong&gt;KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode)"><strong>KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE</strong></a>的大小。 可按如下方式计算：
<p>sizeof (KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE) </p></td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute.SignalProcessingMode</td>
<td>应将 SignalProcessingMode 元素设置为请求的 SIGNALPROCESSINGMODE，例如 AUDIO_SIGNALPROCESSINGMODE_DEFAULT。</td>
</tr>
</tbody>
</table>

 

若要使用 **KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2** ，请定义以下结构。

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
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

 

