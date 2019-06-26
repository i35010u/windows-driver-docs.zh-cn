---
title: WDI_TLV_CREATE_PORT_MAC_ADDRESS
description: WDI_TLV_CREATE_PORT_MAC_ADDRESS 是包含一个 MAC 地址用于 OID_WDI_TASK_CREATE_PORT TLV。
ms.assetid: CE2174E2-CFD7-40E7-B8A2-B96DDB6D6AA4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CREATE_PORT_MAC_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 71e980c4d0e963c06115f182c5ea258deb8cdb8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374707"
---
# <a name="wditlvcreateportmacaddress"></a>WDI\_TLV\_创建\_端口\_MAC\_地址


WDI\_TLV\_创建\_端口\_MAC\_地址是包含的 MAC 地址 TLV [OID\_WDI\_任务\_创建\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)。

## <a name="tlv-type"></a>TLV 类型


0xD9

## <a name="length"></a>长度


大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                   |
|---------------------------------------------------|-----------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 要使用的端口创建的 MAC 地址。 |

 

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

 

 




