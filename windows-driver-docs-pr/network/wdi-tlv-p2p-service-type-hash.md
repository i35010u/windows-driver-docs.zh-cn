---
title: WDI_TLV_P2P_SERVICE_TYPE_HASH
description: WDI_TLV_P2P_SERVICE_TYPE_HASH 是包含服务类型的哈希 TLV。
ms.assetid: A475C2E3-F558-47EC-9708-87887AE2D8AF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_TYPE_HASH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8308a82a3c4298b04a5f067ecb3b03d84187bf07
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355421"
---
# <a name="wditlvp2pservicetypehash"></a>WDI\_TLV\_P2P\_SERVICE\_TYPE\_HASH


WDI\_TLV\_P2P\_服务\_类型\_哈希是包含服务类型的哈希 TLV。

**请注意**  此 TLV 添加 Windows 10，版本 1607，WDI 版本 1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12A

## <a name="length"></a>长度


大小 （以字节为单位） [ **WDI\_P2P\_服务\_名称\_哈希**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash)结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述               |
|-------------------------------------------------------------------------|---------------------------|
| [**WDI\_P2P\_SERVICE\_NAME\_HASH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash) | 服务类型的哈希值。 |

 

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

 

 




