---
title: WDI_TLV_BSS_ENTRY_AGE_INFO
description: WDI_TLV_BSS_ENTRY_AGE_INFO 是包含 BSS 条目的年龄信息 TLV。
ms.assetid: 3D0DC599-2A66-45E9-B02C-32291A028139
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY_AGE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e3672b36a4aa0ec6a9ea2da8f1f80991e7c82218
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387210"
---
# <a name="wditlvbssentryageinfo"></a>WDI\_TLV\_BSS\_ENTRY\_AGE\_INFO


WDI\_TLV\_BSS\_条目\_年龄\_信息是包含 BSS 条目的年龄信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0xBA

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT64</td>
<td>最近发现此 BSS 条目的时间戳。 时间戳应获取与<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetcurrentsystemtime" data-raw-source="[&lt;strong&gt;NdisGetCurrentSystemTime&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetcurrentsystemtime)"> <strong>NdisGetCurrentSystemTime</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerysystemtime" data-raw-source="[&lt;strong&gt;KeQuerySystemTime&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerysystemtime)"> <strong>KeQuerySystemTime</strong></a>。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定此信息是实时的 （当前正在运行的扫描期间找到） 还是来自 IHV 组件的 BSS 列表缓存。
<p>有效值为 0 （实时） 或 1 （已缓存）。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




