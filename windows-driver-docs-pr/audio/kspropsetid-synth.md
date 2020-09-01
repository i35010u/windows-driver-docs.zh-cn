---
title: KSPROPSETID \_ 合成
description: KSPROPSETID \_ 合成
ms.assetid: ff5efd85-0b4d-4625-b029-fecf325bcacb
keywords:
- KSPROPSETID_Synth
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45ef263495bd8885281521de0816a6ce20083e27
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211457"
---
# <a name="kspropsetid_synth"></a>KSPROPSETID \_ 合成


## <span id="ddk_kspropsetid_synth_ks"></span><span id="DDK_KSPROPSETID_SYNTH_KS"></span>


`KSPROPSETID_Synth`属性集包含的属性对于合成节点 ([**KSNODETYPE \_ 合成**](ksnodetype-synthesizer.md)器) 的配置是全局的。

此集中的属性项由 KSPROPERTY \_ 合成枚举值指定，如标头文件 Dmusprop 中所定义。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

\_ \_ 系统使用 KSPROPERTY 合成 cap 属性来确定合成器的功能。

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps" data-raw-source="[&lt;strong&gt;SYNTHCAPS&lt;/strong&gt;](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)"><strong>SYNTHCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 SYNTHCAPS 类型的结构，并指定合成器的功能。 这些功能包括：

-   可用内存量

-   通道组的最大数量

-   最大声音数量

-   最大音频通道数

-   呈现效果

有关详细信息，请参阅 [**SYNTHCAPS**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ cap 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

有关合成器功能的详细信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectMusicPort：： GetCaps** 方法和 dmu \_ PORTCAPS 结构。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

\_ \_ 系统使用 KSPROPERTY 合成 CHANNELGROUPS 属性来设置或获取 pin 实例上活动通道组的数目。 通道组从零开始，在每个 pin 实例上编号。

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型，指定 pin 支持的通道组的数目。 如果 pin 支持 *n* 个通道组，则 pin 上的通道组将从0到 *n*-1 进行编号。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ cap 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的失败代码。

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
<td align="left"><p>缓冲区太小，无法完成操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

有关通道组的详细信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectMusicPort：： GetNumChannelGroups** 和 **IDirectMusicPort：： SetNumChannelGroups** 方法的说明。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ LATENCYCLOCK 属性用于查询微端口驱动程序的当前延迟时间（始终大于主时钟时间）。

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONGLONG</p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (类型为 ULONGLONG，表示合成器的当前滞后时间。 此时间是相对于主时钟指定的，并以100毫微秒为单位表示。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ LATENCYCLOCK 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的失败代码。

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
<td align="left"><p>缓冲区太小，无法完成操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>此设备的操作无效。</p></td>
</tr>
</tbody>
</table>

 

延迟时钟通常用于在多个设备之间同步音频输出流。

KSPROPERTY \_ 合成 \_ LATENCYCLOCK get 属性请求应返回等于当前的主时钟时间的延迟时钟时间，加上流通过的音频筛选器的最小保证延迟。 一种应用程序，用于计划要播放的音频数据早于当前滞后时间的数据风险。

有关延迟时钟的详细信息，请参阅以下内容：

-   \_ \_ [延迟时钟](./latency-clocks.md)中的 KSPROPERTY 合成 LATENCYCLOCK 属性的讨论。

-   Microsoft Windows SDK 文档中的 **IDirectMusicPort：： GetLatencyClock** 和 **IReferenceClock：： GetTime** 方法的说明。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ PORTPARAMETERS 属性用于获取 DirectMusic *端口*的配置参数，它是用于发送或接收音乐数据的设备的 DirectMusic 术语。  (在 KS 术语中，DirectMusic 端口并不对应于 Dmu 端口驱动程序。 它对应于 DirectMusic 筛选器上的呈现或捕获 pin。 ) 

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams" data-raw-source="[&lt;strong&gt;SYNTH_PORTPARAMS&lt;/strong&gt;](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams)"> <strong>SYNTH_PORTPARAMS</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams" data-raw-source="[&lt;strong&gt;SYNTH_PORTPARAMS&lt;/strong&gt;](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams)"><strong>SYNTH_PORTPARAMS</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 包含一个后跟合成 PORTPARAMS 结构的 KSNODEPROPERTY 结构 \_ 。 在发送属性请求之前，客户端通过将其写入合成 PORTPARAMS 结构来指定其请求的参数值 \_ 。

) 操作数据 (的属性值也是合成 PORTPARAMS 类型 \_ 。 微型端口驱动程序使用它实际用于配置端口的参数值加载此结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

如果微型端口驱动程序成功地按调用方指定的方式配置 DirectMusic 端口，则会返回状态 " \_ 成功" 代码。 否则，它将返回相应的错误代码。 下表指出了一些可能的错误状态代码。

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
<td align="left"><p>操作成功，但微型端口驱动程序必须修改调用方在属性值中标记为有效的一个或多个参数值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

这是要处理的 DirectMusic 属性项中最复杂的内容。 尽管此属性仅支持 get 请求，但 get 请求还会设置端口参数。 端口将合成 \_ PORTPARAMS 结构传递为属性请求的属性描述符。 属性-值缓冲区附带了属性请求，但由于这是 get 请求，因此仅用于从微型端口驱动程序中检索信息。

微型端口驱动程序应首先将合成 \_ PORTPARAMS 结构从属性描述符复制到属性值缓冲区。 接下来，应检查它是否能够支持调用方请求的所有参数值 (标记为有效) 。 如果微型端口驱动程序无法支持一个或多个请求的参数值，则它应覆盖 \_ 属性-值缓冲区中的合成 PORTPARAMS 结构中的 (，) 这些特定参数的请求值及其可支持的值。

如果微型端口驱动程序未更改调用方的合成 \_ PORTPARAMS，则调用方应返回与调用方最初向下发送到微型端口驱动程序的属性描述符中的参数完全匹配的属性值。

按照约定，驱动程序还会填充在合成 PORTPARAMS 的 **dwValidParams** 成员中未设置相应位的参数的值 \_ 。 这允许调用方查看微型端口驱动程序用于这些参数的默认值。 微型端口驱动程序输出用于构建波形接口设备的实际参数值。

微型端口驱动程序的 KSPROPERTY \_ 合成 \_ PORTPARAMETERS 处理程序应做好准备，以便正确处理对采样率更改的请求。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ RUNNINGSTATS 属性用于查询小型端口驱动程序的性能统计信息。

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_stats" data-raw-source="[&lt;strong&gt;SYNTH_STATS&lt;/strong&gt;](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_stats)"><strong>SYNTH_STATS</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是合成统计信息类型的结构 \_ 。 微型端口驱动程序的属性处理程序将以下统计信息写入到此结构中：

-   语音播放的平均数量

-   CPU 使用率

-   丢失的注释数

-   可用内存量

-   峰值音量级别

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ RUNNINGSTATS 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
<td align="left"><p>缓冲区太小，无法完成操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>此设备的操作无效。</p></td>
</tr>
</tbody>
</table>

 

当设备仍处于 KSSTATE 运行状态时，合成器的性能统计信息会不断更新 \_ 。 每次设备进入此状态时，它都会重置统计信息，这是零个累计值，如高峰量和丢失的便笺数。

有关其他信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectMusicPort：： GetRunningStats** 方法和 dmu \_ SYNTHSTATS 结构的描述。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ VOICEPRIORITY 属性指定当微型端口驱动程序需要从语音缓存中凹凸声音时，MIDI 合成器中的特定语音应具有的优先级。

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthvoicepriority_instance" data-raw-source="[&lt;strong&gt;SYNTHVOICEPRIORITY_INSTANCE&lt;/strong&gt;](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthvoicepriority_instance)"> <strong>SYNTHVOICEPRIORITY_INSTANCE</strong></a></p></td>
<td align="left"><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 包含一个后跟 SYNTHVOICEPRIORITY 实例结构的 KSNODEPROPERTY 结构，该结构 \_ 指定语音的通道组， (组中的16个 MIDI 通道) 和通道号 (。

) 操作数据 (的属性值是指定优先级的 DWORD 值。 客户端使用 KSPROPERTY \_ 合成 \_ VOICEPRIORITY 集请求将语音的新优先级发送到微型端口驱动程序，并使用 KSPROPERTY \_ 合成 \_ VOICEPRIORITY get-property 请求从微型端口驱动程序检索语音的当前优先级。

**语音优先级**

标头文件 Dmusprop 中定义了以下通道组优先级：

```cpp
  DAUD_CRITICAL_VOICE_PRIORITY
  DAUD_HIGH_VOICE_PRIORITY
  DAUD_STANDARD_VOICE_PRIORITY
  DAUD_LOW_VOICE_PRIORITY
  DAUD_PERSIST_VOICE_PRIORITY
```

前面的列表在列表顶部有最高优先级，最小的顺序排列在底部。 这些优先级与通道优先级偏移量运算，达到通道组中每个通道的语音优先级。 生成的优先级在 get 和 set 属性请求中传递。

与通道优先级偏移量相比，前面的通道组优先级值较大。 结果是，更改通道组优先级会引发或降低整个通道组相对于其他通道组的优先级，而不会改变通道组内通道的相对优先级。

### <a name="span-iddefault_prioritiesspanspan-iddefault_prioritiesspan-default-priorities"></a><span id="default_priorities"></span><span id="DEFAULT_PRIORITIES"></span> 默认优先级

创建合成器微型端口驱动程序时，它会为其每个声音指定默认优先级。 默认值定义如下：

-   默认情况下，各通道组的优先级相等。 例如，这意味着通道组1上的通道5与通道组2上的通道5具有相同的优先级。

-   根据 DLS 第1级规范，通道 10 (MIDI 打击乐器通道) 的优先级最高，后跟1到9，11到16。

标头文件 Dmusprop 定义了以下优先级偏移量：

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

前面的偏移列表在列表顶部按最高优先级排序。 标头文件 Dmusprop 还使用 DAUD \_ 标准语音优先级，定义每个通道组中通道的默认优先级，按位 or \_ \_ 。 例如，下面的定义为每个通道组中的通道1提供默认优先级：

```cpp
  #define DAUD_CHAN1_DEF_VOICE_PRIORITY \
    (DAUD_STANDARD_VOICE_PRIORITY | DAUD_CHAN1_VOICE_PRIORITY_OFFSET)
```

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ VOICEPRIORITY 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
<td align="left"><p>缓冲区太小，无法完成操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

有关语音优先级的详细信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectMusicPort：： GetChannelPriority** 和 **IDirectMusicPort：： SetChannelPriority** 方法的说明。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ VOLUME 属性获取或设置合成器设备的音量级别。

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值的类型为 LONG，并指定合成器设备的音量级别。 卷设置以分贝的 1/100ths 单位来指定。 小型端口驱动程序应更改其卷或报告其卷，具体取决于请求是获取还是设置属性。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ 卷属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
<td align="left"><p>缓冲区太小，无法完成操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
</tbody>
</table>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成器 \_ VOLUMEBOOST 属性指定合成器设备卷的提升量。

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值的类型为 LONG，指定组合阶段后的音频信号的增加量。 这是所有语音 articulation 和混合完成后要添加到合成器最终输出的量。 卷提升量是以分贝的 1/100ths 指定的。 此值可以是正数也可以是负数。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ VOLUMEBOOST 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
<td align="left"><p>缓冲区太小，无法完成操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
</tbody>
</table>


不应将其他提升添加到输出中。 合成器应遵循严格的 DLS 第1级 articulation 约定。

此属性用于将合成器的音量与系统中的其他音频输出均衡，因此，应以一致的方式在所有设备上解释增加的数量。

 

