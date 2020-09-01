---
title: WDI_TLV_BSS_ENTRY_AGE_INFO
description: WDI_TLV_BSS_ENTRY_AGE_INFO 是包含 BSS 条目的 AGE 信息的 TLV。
ms.assetid: 3D0DC599-2A66-45E9-B02C-32291A028139
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY_AGE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4a974ffc6602d2279a099af19b6209b66bd05ee0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216814"
---
# <a name="wdi_tlv_bss_entry_age_info"></a>WDI \_ TLV \_ BSS \_ 条目 \_ AGE \_ 信息


WDI \_ tlv \_ bss \_ 条目 \_ AGE \_ 信息是包含 BSS 条目的 age 信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xBA

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT64</td>
<td>此 BSS 条目最近发现时的时间戳。 应通过 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetcurrentsystemtime" data-raw-source="[&lt;strong&gt;NdisGetCurrentSystemTime&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetcurrentsystemtime)"><strong>NdisGetCurrentSystemTime</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime" data-raw-source="[&lt;strong&gt;KeQuerySystemTime&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)"><strong>KeQuerySystemTime</strong></a>获取时间戳。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定在当前运行的) 扫描期间 (找到此信息，还是来自 IHV 组件的 BSS 列表缓存。
<p>有效值为 0 (实时) 或 1 (缓存) 。</p></td>
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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

