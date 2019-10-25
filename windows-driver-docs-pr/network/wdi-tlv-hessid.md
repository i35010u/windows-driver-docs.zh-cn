---
title: WDI_TLV_HESSID
description: WDI_TLV_HESSID 是包含 HESSIDs 列表的 TLV。
ms.assetid: 630A1824-7722-4B03-8073-EFC44E142400
ms.date: 07/18/2017
keywords:
- WDI_TLV_HESSID 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 671f8209f35441afe7c09192b66457bd233f680e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844204"
---
# <a name="wdi_tlv_hessid"></a>WDI\_TLV\_HESSID


WDI\_TLV\_HESSID 是包含 HESSIDs 列表的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xC8

## <a name="length"></a>长度


WDI 数组的大小（以字节为单位） [ **\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                  | 描述        |
|-------------------------------------------------------|--------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | HESSIDs 的列表。 |

 

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
<td><p>Windows 10</p></td>
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

 

 




