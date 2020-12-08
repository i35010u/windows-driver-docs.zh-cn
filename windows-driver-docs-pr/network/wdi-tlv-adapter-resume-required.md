---
title: WDI_TLV_ADAPTER_RESUME_REQUIRED
description: WDI_TLV_ADAPTER_RESUME_REQUIRED 是一种 TLV，用于指定是否需要重新开始适配器。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADAPTER_RESUME_REQUIRED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a41abf72da292a48240afc0228a9c01a66aea354
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822041"
---
# <a name="wdi_tlv_adapter_resume_required"></a>WDI \_ TLV \_ 适配器 \_ \_ 需要恢复


\_需要 WDI tlv \_ 适配器 \_ 恢复 \_ 是一个 tlv，用于指定是否需要重新开始适配器。

## <a name="tlv-type"></a>TLV 类型


0xB7

## <a name="length"></a>长度


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>指定是否需要重新开始适配器。
<p>有效值为 0 (不需要) 和 1 (必需) 。 如果设置为1，则固件需要 OS 帮助才能恢复其上下文。</p></td>
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




