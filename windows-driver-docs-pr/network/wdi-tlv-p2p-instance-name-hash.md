---
title: WDI_TLV_P2P_INSTANCE_NAME_HASH
description: WDI_TLV_P2P_INSTANCE_NAME_HASH 是一个 TLV，其中包含 "Instance Name，Service Type" 的哈希值。
ms.assetid: A29D0339-93A8-43EB-8C22-DD7A7DC2147C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INSTANCE_NAME_HASH 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5d09bd603504b959b4d640a26dc4c29a40488493
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842359"
---
# <a name="wdi_tlv_p2p_instance_name_hash"></a>WDI\_TLV\_P2P\_实例\_名称\_哈希


WDI\_TLV\_P2P\_实例\_名称\_哈希是包含 "Instance Name，Service Type" 哈希的 TLV。

**请注意**  此 TLV 添加到了 Windows 10 1607 版 WDI 版本1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12C

## <a name="length"></a>长度


WDI 的大小（以字节为单位） [ **\_P2P\_SERVICE\_名称\_哈希**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash)结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述                                |
|-------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_P2P\_服务\_名称\_哈希**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash) | "Instance Name，Service Type" 的哈希。 |

 

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

 

 




