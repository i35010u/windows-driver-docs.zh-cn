---
title: KSPROPSETID\_合成器\_Dls
description: KSPROPSETID\_合成器\_Dls
ms.assetid: 8d6038bf-1ec4-4120-9815-d1e6b7994f33
keywords:
- KSPROPSETID_Synth_Dls
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8048abb14498e3a9bf0c4a8c15fe4bb68e73637d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332479"
---
# <a name="kspropsetidsynthdls"></a>KSPROPSETID\_合成器\_Dls


## <span id="ddk_kspropsetid_synth_dls_ks"></span><span id="DDK_KSPROPSETID_SYNTH_DLS_KS"></span>


`KSPROPSETID_Synth_Dls`属性集包含用于下载 DLS 示例和 instruments 到 MIDI 合成器的属性。 这些是合成器节点的属性 ([**KSNODETYPE\_合成器**](ksnodetype-synthesizer.md)) DirectMusic 筛选器对 DirectMusic pin (请参阅[MIDI 和 DirectMusic 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff537520)).

本部分介绍有关如何下载并卸载"块"包含 DLS 数据的内存的这些属性的行为。 Microsoft Windows SDK 文档中的低级别 DLS 讨论中指定的已下载的检测和批数据区块的实际格式。

DLS 下载并卸载可以出现的 pin 存在任何时间。 不同于 DirectMusic 事件，它们不是时间戳，并应尽可能快地处理。

在本部分中，术语 DLS 资源或只是资源，引用 DLS 检测区块或 DLS 批区块。 系统能正确维护所有 DLS 资源上的引用计数：

-   客户端卸载引用批的最后一个工具，系统会自动生成卸载波次的调用。

-   相反，系统将推迟调用卸载批，直到客户端卸载引用批的最后一个工具。

在此集中的属性项由 KSPROPERTY\_合成器\_DLS 枚举值，如标头中定义文件 Dmusprop.h。

## <span id="ddk_ksproperty_synth_dls_append_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_APPEND_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成\_DLS\_追加属性指定客户端将追加到其下载到合成器每个缓冲区中的 DLS 数据的保留的存储空间量。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型为 ULONG，指定的微型端口驱动程序需要为每个已下载的 DLS 数据缓冲区的末尾使用保留的字节数。 然后，客户端分配每个下载缓冲区足够大，若要下载的数据结束后包含请求的字节数。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_DLS\_追加属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

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
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

这些附加的字节适用的驱动程序，需要额外的填充对齐要求，或复制的一个示例开始，为了简化示例内插。

## <span id="ddk_ksproperty_synth_dls_compact_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_COMPACT_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成\_DLS\_COMPACT 属性是合成器提供免费的示例内存的最大可能块区的请求。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

没有属性值 （操作数据） 是与此属性相关联。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_DLS\_COMPACT 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

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
<td align="left"><p>该操作未成功完成。</p></td>
</tr>
</tbody>
</table>

 

此属性的处理程序的实现应不会中断播放。

有关详细信息，请参阅的说明**IDirectMusicPort::Compact** Microsoft Windows SDK 文档中的方法。

## <span id="ddk_ksproperty_synth_dls_download_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_DOWNLOAD_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成\_DLS\_下载属性用于 DLS 数据下载到合成器。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://msdn.microsoft.com/library/windows/hardware/ff538460" data-raw-source="[&lt;strong&gt;SYNTH_BUFFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538460)"><strong>SYNTH_BUFFER</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538429" data-raw-source="[&lt;strong&gt;SYNTHDOWNLOAD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538429)"><strong>SYNTHDOWNLOAD</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 包含后紧跟着合成器的 KSNODEPROPERTY 结构\_缓冲区结构，它指定的位置和正在下载 DLS 数据缓冲区的大小。

属性值 （操作数据） 是 SYNTHDOWNLOAD 结构。 微型端口驱动程序将返回传递此结构中的以下信息：

-   微型端口驱动程序来唯一标识已下载的 DLS 数据将生成一个句柄。 此客户端应该保存此句柄和更高版本使用它来卸载数据 (请参阅[ **KSPROPERTY\_合成\_DLS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff537398))。

-   一个布尔值，该值指示是否在客户端可以释放包含 DLS 数据属性请求完成后的缓冲区。 如果微型端口驱动程序做了其自己 DLS 数据副本，则客户端可以释放缓冲区。 否则，如果微型端口驱动程序将继续使用客户端的原始 DLS 数据缓冲区，客户端应不释放缓冲区之前微型端口驱动程序卸载 DLS 数据。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_DLS\_下载属性请求返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

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
<td align="left"><p>STATUS_NO_MEMORY</p></td>
<td align="left"><p>内存不可用来完成此请求。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅的讨论**IDirectMusicPort::DownloadInstrument** Microsoft Windows SDK 文档中的方法。

**示例**

KSPROPERTY\_合成\_DLS\_下载属性请求指定的 DLS 位置下载数据与用户内存地址。 微型端口驱动程序应探测并锁定包含 DLS 数据，然后再尝试访问它的用户内存。 下面的示例代码演示如何执行此操作：

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

## <span id="ddk_ksproperty_synth_dls_unload_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_UNLOAD_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成\_DLS\_卸载属性卸载以前下载的 DLS 数据资源。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>句柄</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值的类型句柄，并包含是要释放的已下载 DLS 数据资源的句柄。 这是微型端口驱动程序生成的标识 DLS 数据在上一次的句柄[ **KSPROPERTY\_合成\_DLS\_下载**](https://msdn.microsoft.com/library/windows/hardware/ff537396)get 属性请求.

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_DLS\_卸载属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

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
<td align="left"><p>STATUS_PENDING</p></td>
<td align="left"><p>在更高版本时将完成该操作。</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序应卸载 DLS 数据，因为没有播放，没有说明使用 DLS 数据。 如果合成器不能释放 KSPROPERTY 时与 DLS 数据资源相关联的内存\_合成\_DLS\_请求卸载设置属性，它可以使用异步属性完成来完成请求在更高版本时。

如果卸载 DLS 数据资源后, 合成器收到注意在事件使用的资源时，微型端口驱动程序应忽略该事件，除非已在此期间下载新的 DLS 数据资源。

有关详细信息，请参阅的讨论**IDirectMusicPort::UnloadInstrument** Microsoft Windows SDK 文档中的方法。

## <span id="ddk_ksproperty_synth_dls_waveformat_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_WAVEFORMAT_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成\_DLS\_WAVEFORMAT 属性用于查询有关其输出波形格式合成器。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538799" data-raw-source="[&lt;strong&gt;WAVEFORMATEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538799)"><strong>WAVEFORMATEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值类型 WAVEFORMATEX 的是，它指定合成器的输出流的波形格式。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_DLS\_WAVEFORMAT 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了一些可能的错误代码。

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
</tbody>
</table>

 

属性值的缓冲区**sizeof**(WAVEFORMATEX) 字节不可能足够大，对所有波形格式。 例如，多渠道格式需要的缓冲区**sizeof**([**WAVEFORMATEXTENSIBLE**](https://msdn.microsoft.com/library/windows/hardware/ff538802)) 字节。 如果属性请求将返回状态代码的状态\_缓冲区\_过\_小，客户端可以检查微型端口驱动程序输出的属性值大小、 分配较大的缓冲区，然后提交的第二个请求。

有关详细信息，请参阅的说明**IDirectMusicPort::GetFormat** Microsoft Windows SDK 文档中的方法。

 

 





