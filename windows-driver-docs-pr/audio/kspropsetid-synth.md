---
title: KSPROPSETID\_合成器
description: KSPROPSETID\_合成器
ms.assetid: ff5efd85-0b4d-4625-b029-fecf325bcacb
keywords:
- KSPROPSETID_Synth
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 205d9ee065972cb55732d91f0b5c5a1f59a2818b
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391579"
---
# <a name="kspropsetidsynth"></a>KSPROPSETID\_合成器


## <span id="ddk_kspropsetid_synth_ks"></span><span id="DDK_KSPROPSETID_SYNTH_KS"></span>


`KSPROPSETID_Synth`属性集包含的属性的全局合成器节点的配置 ([**KSNODETYPE\_合成器**](ksnodetype-synthesizer.md))。

在此集中的属性项由 KSPROPERTY\_合成器的枚举值，如标头中定义文件 Dmusprop.h。

## <span id="ddk_ksproperty_synth_caps_ks"></span><span id="DDK_KSPROPERTY_SYNTH_CAPS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成器\_系统使用 CAPS 属性来确定合成器的功能。

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthcaps" data-raw-source="[&lt;strong&gt;SYNTHCAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthcaps)"><strong>SYNTHCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型 SYNTHCAPS 的结构，它指定合成器的功能。 这些功能包括：

-   示例可用的内存量

-   最大通道组数

-   语音的最大数目

-   最大音频通道数

-   呈现效果

有关详细信息，请参阅[ **SYNTHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthcaps)。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_CAPS 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

合成器功能的详细信息，请参阅**IDirectMusicPort::GetCaps**方法和 DMU\_PORTCAPS 结构中 Microsoft Windows SDK 文档。

## <span id="ddk_ksproperty_synth_channelgroups_ks"></span><span id="DDK_KSPROPERTY_SYNTH_CHANNELGROUPS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成器\_系统使用 CHANNELGROUPS 属性来设置或获取 pin 实例上的可用通道组数。 通道组编号，从零，每个 pin 实例上。

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型为 ULONG，指定多少通道进行分组的 pin 支持。 如果 pin 支持*n*通道组的插针通道组的编号介于 0 到*n*-1。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_CAPS 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的失败代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>缓冲区太小，无法完成该操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

有关通道组的详细信息，请参阅的说明**IDirectMusicPort::GetNumChannelGroups**并**IDirectMusicPort::SetNumChannelGroups** Microsoft Windows SDK 中的方法文档。

## <span id="ddk_ksproperty_synth_latencyclock_ks"></span><span id="DDK_KSPROPERTY_SYNTH_LATENCYCLOCK_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成器\_LATENCYCLOCK 属性用来查询流的当前延迟时钟时间，即始终大于 master 时钟时间的微型端口驱动程序。

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONGLONG</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 ULONGLONG，表示合成器的当前延迟时间。 此时间是指定相对于主时钟，以 100 毫微秒为单位表示。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_LATENCYCLOCK 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的失败代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>缓冲区太小，无法完成该操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>该操作对于此设备无效。</p></td>
</tr>
</tbody>
</table>

 

延迟时钟通常用于将音频输出流到多个设备同步。

KSPROPERTY\_合成器\_LATENCYCLOCK 属性 get 请求应返回延迟时钟时间等于当前的主时钟时间，加上所需的最低保证音频筛选器通过流传递的延迟。 计划要早于当前延迟时钟时间风险数据晚播放播放的音频数据的应用程序。

有关延迟时钟的详细信息，请参阅：

-   讨论 KSPROPERTY\_合成\_LATENCYCLOCK 属性中的[延迟时钟](https://docs.microsoft.com/windows-hardware/drivers/audio/latency-clocks)。

-   说明**IDirectMusicPort::GetLatencyClock**并**IReferenceClock::GetTime** Microsoft Windows SDK 文档中的方法。

## <span id="ddk_ksproperty_synth_portparameters_ks"></span><span id="DDK_KSPROPERTY_SYNTH_PORTPARAMETERS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成\_PORTPARAMETERS 属性用于获取配置参数的 DirectMusic*端口*，这是发送或接收音乐数据的设备的 DirectMusic 术语。 （在 KS 术语中，DirectMusic 端口不对应 Dmu 端口驱动程序。 它对应于 DirectMusic 筛选器上呈现或捕获的 pin。）

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_portparams" data-raw-source="[&lt;strong&gt;SYNTH_PORTPARAMS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_portparams)"><strong>SYNTH_PORTPARAMS</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_portparams" data-raw-source="[&lt;strong&gt;SYNTH_PORTPARAMS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_portparams)"><strong>SYNTH_PORTPARAMS</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 包含后紧跟着合成器的 KSNODEPROPERTY 结构\_PORTPARAMS 结构。 在发送前属性请求，客户端指定其请求的参数值写入到合成器通过\_PORTPARAMS 结构。

属性值 （操作数据） 也属于类型合成器\_PORTPARAMS。 微型端口驱动程序将加载此结构与它实际上使用可配置的端口的参数值。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

如果在配置严格按照指定由调用方 DirectMusic 端口成功微型端口驱动程序，它将返回状态\_成功代码。 否则，它返回相应的错误代码。 下表列出一些可能的错误状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_NOT_ALL_ASSIGNED</p></td>
<td align="left"><p>操作成功，但微型端口驱动程序必须修改一个或多个调用方标记为在属性值中有效的参数值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

这是最复杂的要处理的 DirectMusic 属性项。 此属性支持仅 get 请求，但 get 请求还设置端口参数。 端口通过合成器\_PORTPARAMS 结构作为属性请求的属性描述符。 属性值缓冲区附带属性请求，但由于这是 get 请求，缓冲区仅用于从微型端口驱动程序中检索信息。

微型端口驱动程序应首先复制合成器\_PORTPARAMS 结构从属性描述符的属性值的缓冲区。 接下来，它应检查以查看它是否能够支持所有参数值调用方请求 （标记为有效）。 如果微型端口驱动程序不能支持一个或多个请求的参数值，它应覆盖 (中合成器\_PORTPARAMS 结构中的属性值缓冲区) 请求的值为这些特定参数的值，它可以支持。

如果微型端口驱动程序进行任何更改到调用方的合成器\_PORTPARAMS，调用方应得到与调用方最初发送给微型端口驱动程序的属性描述符中的参数完全匹配的属性值。

按照约定，该驱动程序还会填写不具有相应的位设置的参数的值**dwValidParams**合成器的成员\_PORTPARAMS。 这允许调用方以查看哪些默认值用于这些参数的微型端口驱动程序。 微型端口驱动程序输出使用它来生成批接口设备的实际参数值。

微型端口驱动程序的 KSPROPERTY\_合成器\_PORTPARAMETERS 处理程序应做好正确处理采样率更改的请求。

## <span id="ddk_ksproperty_synth_runningstats_ks"></span><span id="DDK_KSPROPERTY_SYNTH_RUNNINGSTATS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成器\_RUNNINGSTATS 属性用于查询合成器的性能统计信息的微型端口驱动程序。

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_stats" data-raw-source="[&lt;strong&gt;SYNTH_STATS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_stats)"><strong>SYNTH_STATS</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构类型合成器的\_统计信息。 微型端口驱动程序的属性处理程序将以下统计信息写入到此结构：

-   播放的声音的平均数目

-   CPU 使用率

-   丢失的说明的数量

-   可用内存量

-   峰值音量级别

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_RUNNINGSTATS 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>缓冲区太小，无法完成该操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>该操作对于此设备无效。</p></td>
</tr>
</tbody>
</table>

 

合成器的性能统计信息会不断更新时，设备仍保持 KSSTATE\_运行状态。 每次设备将进入此状态时，它将重置统计信息，如峰值卷和数的累积值零的处理方法的丢失的说明。

有关其他信息，请参阅的说明**IDirectMusicPort::GetRunningStats**方法和 DMU\_SYNTHSTATS 结构中 Microsoft Windows SDK 文档。

## <span id="ddk_ksproperty_synth_voicepriority_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOICEPRIORITY_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成器\_VOICEPRIORITY 属性指定从其语音缓存语音微型端口驱动程序需要使用以便将服务器数量时，应具有 MIDI 合成器中的特定语音何种优先级。

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthvoicepriority_instance" data-raw-source="[&lt;strong&gt;SYNTHVOICEPRIORITY_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthvoicepriority_instance)"><strong>SYNTHVOICEPRIORITY_INSTANCE</strong></a></p></td>
<td align="left"><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 包含后紧跟着 SYNTHVOICEPRIORITY KSNODEPROPERTY 结构\_实例结构，它指定语音的通道组 （16 个 MIDI 通道的集） 和通道数字 （在组中）。

属性值 （操作数据） 是一个 dword 值，指定的优先级。 客户端使用 KSPROPERTY\_合成\_VOICEPRIORITY 集属性请求将发送到微型端口驱动程序，和它的语音的新优先级使用 KSPROPERTY\_合成器\_VOICEPRIORITY 属性 get 请求到从微型端口驱动程序检索语音的当前优先级。

**语音优先级**

标头文件 Dmusprop.h 中定义的以下通道组优先级：

```cpp
  DAUD_CRITICAL_VOICE_PRIORITY
  DAUD_HIGH_VOICE_PRIORITY
  DAUD_STANDARD_VOICE_PRIORITY
  DAUD_LOW_VOICE_PRIORITY
  DAUD_PERSIST_VOICE_PRIORITY
```

前面的列表进行排序最高优先级列表的顶部和底部最低。 这些优先级是到达通道组中每个通道的语音优先级的通道优先级偏移量或运算。 生成的优先级在 get 和 set 属性请求中传递。

前面的通道组优先级值为大到通道优先级偏移量进行比较。 结果是该更改通道组优先级引发或降低整个通道组相对于其他通道组的优先级，而无需更改通道组中的通道的相对优先级。

### <a name="span-iddefaultprioritiesspanspan-iddefaultprioritiesspan-default-priorities"></a><span id="default_priorities"></span><span id="DEFAULT_PRIORITIES"></span> 默认优先级

创建合成器微型端口驱动程序时，它将默认优先级分配给每个其语音。 默认值定义，如下所示：

-   默认情况下，优先级相等跨通道组。 例如，这意味着该通道 5 通道组 1 上的有与通道组 2 上的通道 5 相同的优先级。

-   DLS 级别 1 规范根据频道 10 （MIDI 打击乐器频道） 具有最高优先级，跟 1 到 9 和 11 到 16。

标头文件 Dmusprop.h 定义以下优先级偏移量：

```cpp
  DAUD_CHAN10_VOICE_PRIORITY_OFFSET
  DAUD_CHAN1_VOICE_PRIORITY_OFFSET
  DAUD_CHAN2_VOICE_PRIORITY_OFFSET
  DAUD_CHAN3_VOICE_PRIORITY_OFFSET
  DAUD_CHAN4_VOICE_PRIORITY_OFFSET
  DAUD_CHAN5_VOICE_PRIORITY_OFFSET
  DAUD_CHAN6_VOICE_PRIORITY_OFFSET
  DAUD_CHAN7_VOICE_PRIORITY_OFFSET
  DAUD_CHAN8_VOICE_PRIORITY_OFFSET
  DAUD_CHAN9_VOICE_PRIORITY_OFFSET
  DAUD_CHAN11_VOICE_PRIORITY_OFFSET
  DAUD_CHAN12_VOICE_PRIORITY_OFFSET
  DAUD_CHAN13_VOICE_PRIORITY_OFFSET
  DAUD_CHAN14_VOICE_PRIORITY_OFFSET
  DAUD_CHAN15_VOICE_PRIORITY_OFFSET
  DAUD_CHAN16_VOICE_PRIORITY_OFFSET
```

在列表顶部的最高优先级顺序是前面列出的各偏移量。 标头文件 Dmusprop.h 还可以通过按位 or 操作每个偏移量 DAUD 与每个通道组中定义的信道的默认优先级\_标准\_语音\_优先级。 例如，以下定义向每个通道组中的通道 1 的默认优先级：

```cpp
  #define DAUD_CHAN1_DEF_VOICE_PRIORITY \
    (DAUD_STANDARD_VOICE_PRIORITY | DAUD_CHAN1_VOICE_PRIORITY_OFFSET)
```

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_VOICEPRIORITY 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>缓冲区太小，无法完成该操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

有关语音优先级的详细信息，请参阅的说明**IDirectMusicPort::GetChannelPriority**并**IDirectMusicPort::SetChannelPriority** Microsoft Windows SDK 中的方法文档。

## <span id="ddk_ksproperty_synth_volume_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOLUME_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成器\_卷属性获取或设置合成器设备的卷级别。

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 long 类型的值，指定合成器设备的卷级别。 1/100ths 的分贝为单位指定卷设置。 微型端口驱动程序应更改其卷，或者报告其卷，具体取决于该请求是要获取或设置该属性。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_卷属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>缓冲区太小，无法完成该操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

## <span id="ddk_ksproperty_synth_volumeboost_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOLUMEBOOST_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成器\_VOLUMEBOOST 属性指定的量的提升合成器设备的卷。

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 LONG 类型，指定时间量，以组合阶段后提升音频信号。 这是要在所有语音清晰表述后添加到合成器的最终输出量，混合使用已完成。 在 1/100ths 分贝的指定卷提升量。 此值可以为正数或负数。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_VOLUMEBOOST 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>缓冲区太小，无法完成该操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

没有其他 boost 应添加到输出。 合成器应遵循严格的 DLS 一级约定为清晰表述。

此属性用于在系统中，均衡与其他音频输出合成器的卷，因此一致的方式应提升量解释在所有设备上。

 

 





