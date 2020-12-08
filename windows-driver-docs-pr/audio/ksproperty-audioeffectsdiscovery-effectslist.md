---
title: KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST
description: KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST 属性指定静音节点上的通道是否 (静音) 静音 \_ 。
keywords:
- KSPROPERTY_AUDIOEFFECTSDISCOVERY_EFFECTSLIST 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOEFFECTSDISCOVERY_EFFECTSLIST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: a2fae33153d238a7a081830f3f54601fe1be9248
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798961"
---
# <a name="ksproperty_audioeffectsdiscovery_effectslist"></a>KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST

**KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST** 属性是一个筛选器属性，其值是应用于特定 KS pin 工厂的音频效果类型的列表，适用于特定的音频信号处理路径。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

### <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
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
<td><p>通过筛选器实例 (固定工厂) </p></td>
<td><p>KSP_PIN</p></td>
<td><a href="/windows/win32/api/msapofxproxy/ns-msapofxproxy-ksp_pinmode"><strong>KSP_PINMODE</strong></a></td>
</tr>
</tbody>
</table>

属性值是零个或多个音频效果类型 Guid 的数组 (例如，音频 \_ 效果 \_ 类型 \_ 声音 \_ 回声 \_ 取消) ，后者是由 **KSP \_ PINMODE** 结构标识的 pin 信号处理路径中的。

**注意** \_ \_ 不得为此属性设置 KSPROPERTY 类型拓扑标志位。

### <a name="return-value"></a>返回值

**KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST** 属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，此属性请求将返回相应的错误状态代码。

## <a name="remarks"></a>备注

如果音频驱动程序使用 Microsoft 的通用代理 APO 来检索用于 KS pin 的不同信号处理路径中包含的音频效果，则它必须支持此属性。 一般代理 APO 包含在 *msapofxproxy.dll* 文件中。 音频驱动程序可以在音频驱动程序中完成所有信号处理时，或在相应的数字信号处理器 (DSP) 硬件组件中完成所有信号处理，而不是在 APO 中进行任何处理时，使用此通用代理 APO。 在这种情况下，APO 的唯一功能是向音频系统报告信号处理效果。

一般代理 APO 从音频驱动程序接收 **KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST** ，并使用它向音频系统报告效果。 一般代理 APO 假设启用了 KS pin 的筛选器接口时效果列表不会发生更改。

如果属性描述符指定的 KS pin 不支持 **KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST**，则驱动程序必须返回状态 " \_ 不 \_ 受支持"。

如果该属性描述符指定了驱动程序不支持的 *AudioProcessingMode* 值，则驱动程序必须返回 STATUS STATUS \_ \_ 参数。 请注意，音频驱动程序必须支持 [**KSPROPERTY \_ AUDIOSIGNALPROCESSING \_ 模式**](ksproperty-audiosignalprocessing-modes.md) 属性，才能指示其支持的音频信号处理模式。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Msapofxproxy</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**KSP \_ PINMODE**](/windows/win32/api/msapofxproxy/ns-msapofxproxy-ksp_pinmode)

[**KSPROPERTY \_ AUDIOSIGNALPROCESSING \_ 模式**](ksproperty-audiosignalprocessing-modes.md)
