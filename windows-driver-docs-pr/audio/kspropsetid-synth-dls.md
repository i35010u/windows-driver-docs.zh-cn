---
title: KSPROPSETID \_ 合成 \_ dl
description: KSPROPSETID \_ 合成 \_ dl
keywords:
- KSPROPSETID_Synth_Dls
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1b03d97a62cb4e5fa01a2e4313e8f46fbab4f90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801075"
---
# <a name="kspropsetid_synth_dls"></a>KSPROPSETID \_ 合成 \_ dl


## <span id="ddk_kspropsetid_synth_dls_ks"></span><span id="DDK_KSPROPSETID_SYNTH_DLS_KS"></span>


`KSPROPSETID_Synth_Dls`属性集包含用于将 DLS 示例和乐器下载到 MIDI 合成器的属性。 这些是合成节点的属性 ([**KSNODETYPE \_ 合成**](ksnodetype-synthesizer.md) 器) DirectMusic 筛选器的 DirectMusic pin 上 (参阅 [MIDI 和 DirectMusic 筛选器](./midi-and-directmusic-filters.md)) 。

本部分介绍了这些属性的行为，它们与它们如何下载和卸载包含 DLS 数据的内存的 "区块" 有关。 在 Microsoft Windows SDK 文档中的低级 DL 讨论中指定了下载的检测和波形数据区块的实际格式。

在 pin 存在的过程中，可以随时进行 DL 下载和卸载。 与 DirectMusic 事件不同，它们没有时间戳，应尽快处理。

在本部分中，术语 "DL 资源" 或 "仅资源" 是指 DL 检测区块或 DLS 波纹块。 系统在所有 DLS 资源上正确维护引用计数：

-   当客户端卸载引用波形的最后一个检测时，系统会自动生成一个调用来卸载波形。

-   相反，系统会在客户端卸载引用 wave 的最后一个检测之前，延迟对的调用以卸载波形。

此集中的属性项由 KSPROPERTY \_ 合成 \_ dl 枚举值指定，如标头文件 Dmusprop 中所定义。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ dl \_ APPEND 属性指定客户端在其下载到合成器的每个缓冲区中附加到 DLS 数据的保留存储空间量。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型，它指定了在每次下载的 DLS 数据缓冲区结束时，微型端口驱动程序需要保留的字节数。 然后，客户端分配每个下载缓冲区，使其足以在下载的数据结束后包含请求的字节数。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ dl \_ APPEND 属性请求返回状态 SUCCESS，指示该请求已 \_ 成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

这些额外的字节用于需要额外填充以实现对齐要求的驱动程序，或者用于复制示例的开头以便简化示例内插。


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ dl \_ COMPACT 属性是对合成器的请求，使其能够提供尽可能大的可用内存内存块。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

没有属性值 (操作数据) 与此属性关联。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ dl \_ COMPACT 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

此属性的处理程序的实现不应中断播放。

有关详细信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectMusicPort：： Compact** 方法说明。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ dl \_ 下载属性用于将 DLS 数据下载到合成器。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a> + <a href="/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_buffer" data-raw-source="[&lt;strong&gt;SYNTH_BUFFER&lt;/strong&gt;](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_buffer)"> <strong>SYNTH_BUFFER</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthdownload" data-raw-source="[&lt;strong&gt;SYNTHDOWNLOAD&lt;/strong&gt;](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthdownload)"><strong>SYNTHDOWNLOAD</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 包含一个后跟合成缓冲结构的 KSNODEPROPERTY 结构，该结构 \_ 指定正在下载的 DLS 数据缓冲区的位置和大小。

) 操作数据 (的属性值是 SYNTHDOWNLOAD 结构。 微型端口驱动程序会将以下信息传递回此结构：

-   小型端口驱动程序生成的句柄，用于唯一标识下载的 DLS 数据。 此客户端应保存此句柄，稍后再使用它来卸载数据 (请参阅 [**KSPROPERTY \_ 合成 \_ dl \_ unload**](/previous-versions/ff537398(v=vs.85))) 。

-   一个布尔值，该值指示客户端是否可以在属性请求完成后释放包含 DLS 数据的缓冲区。 如果微型端口驱动程序已创建自己的 DLS 数据副本，则客户端可以释放缓冲区。 否则，如果微型端口驱动程序继续使用客户端的原始 DLS 数据缓冲区，则在微型端口驱动程序卸载 DLS 数据之前，客户端不应释放缓冲区。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ dl \_ 下载属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
<td align="left"><p>STATUS_NO_MEMORY</p></td>
<td align="left"><p>没有可用于完成此请求的内存。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectMusicPort：:D ownloadinstrument** 方法的讨论。

**示例**

KSPROPERTY \_ 合成 \_ dl \_ 下载属性请求指定 DLS 使用用户内存地址下载数据的位置。 小型端口驱动程序在尝试访问之前，应探测并锁定包含 DLS 数据的用户内存。 下面的示例代码演示如何执行此操作：

```cpp
  NTSTATUS Status = STATUS_UNSUCCESSFUL;
  PSYNTH_BUFFER pDlsBuffer = (PSYNTH_BUFFER)pRequest->Instance;
  PMDL pMdl = IoAllocateMdl(pDlsBuffer->BufferAddress, pDlsBuffer->BufferSize,
                            FALSE, FALSE, NULL);
  if (pMdl)
  {
      __try
      {
          MmProbeAndLockPages(pMdl, KernelMode, IoReadAccess);
          PVOID pvUserData = MmGetSystemAddressForMdlSafe(pMdl, NormalPagePriority);
 
         // do something with the data here
      }
      __except (EXCEPTION_EXECUTE_HANDLER)
      {
          Status = GetExceptionCode();
      }
 
      MmUnlockPages(pMdl);
      IoFreeMdl(pMdl);
  }
  else
  {
      Status = STATUS_NO_MEMORY;
  }
```

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ dl \_ UNLOAD 属性卸载之前下载的 dls 数据资源。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>句柄</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值为 HANDLE 类型，并且包含要释放的已下载 DLS 数据资源的句柄。 这是微型端口驱动程序生成的用于标识先前 [**KSPROPERTY \_ 合成 \_ DL \_**](/previous-versions/ff537396(v=vs.85))中的 dls 数据的句柄。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ dl \_ UNLOAD 属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
<td align="left"><p>STATUS_PENDING</p></td>
<td align="left"><p>操作将在稍后完成。</p></td>
</tr>
</tbody>
</table>

 

如果没有播放使用 DLS 数据的笔记，微型端口驱动程序应立即卸载 DLS 数据。 如果合成器在 KSPROPERTY 合成 dl 卸载 set 属性请求时无法释放与 DLS 数据资源关联的内存 \_ \_ \_ ，则它可以使用异步属性完成来稍后完成请求。

如果在卸载 DLS 数据资源后，合成器会接收到使用该资源的注释，则微型端口驱动程序应忽略该事件，除非已在临时下载新的 DLS 数据资源。

有关详细信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectMusicPort：： UnloadInstrument** 方法的讨论。


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ DLS \_ WAVEFORMAT 属性用于查询合成器的输出波形格式。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/mmreg/ns-mmreg-waveformatex" data-raw-source="[&lt;strong&gt;WAVEFORMATEX&lt;/strong&gt;](/windows/win32/api/mmreg/ns-mmreg-waveformatex)"><strong>WAVEFORMATEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (类型为 WAVEFORMATEX，并指定合成器输出流的波浪格式。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ dl \_ WAVEFORMAT 属性请求返回状态 " \_ 成功" 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。 下表列出了一些可能的错误代码。

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
</tbody>
</table>


**Sizeof** (WAVEFORMATEX) 字节的属性值缓冲区对于所有波形格式可能不够大。 例如，多通道格式要求使用 **sizeof** ([**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)) 字节的缓冲区。 如果属性请求返回的状态代码 \_ \_ 太 \_ 小，则客户端可以检查微型端口驱动程序输出的属性-值大小，分配更大的缓冲区，然后提交第二个请求。

有关详细信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectMusicPort：： iformatprovider.getformat** 方法说明。
