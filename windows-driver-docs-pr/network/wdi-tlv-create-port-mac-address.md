---
title: WDI_TLV_CREATE_PORT_MAC_ADDRESS
description: WDI_TLV_CREATE_PORT_MAC_ADDRESS 是一个 TLV，其中包含 OID_WDI_TASK_CREATE_PORT 的 MAC 地址。
ms.assetid: CE2174E2-CFD7-40E7-B8A2-B96DDB6D6AA4
ms.date: 07/18/2017
keywords:
- WDI_TLV_CREATE_PORT_MAC_ADDRESS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: efadf719fc3ceb0da04249b425b2a256351e6cea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833844"
---
# <a name="wdi_tlv_create_port_mac_address"></a>WDI\_TLV\_创建\_端口\_MAC\_地址


WDI\_TLV\_创建\_端口\_MAC\_地址是包含 OID MAC 地址的 TLV [\_WDI\_TASK\_创建\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)。

## <a name="tlv-type"></a>TLV 类型


0xD9

## <a name="length"></a>长度


[**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                   |
|---------------------------------------------------|-----------------------------------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 要用于端口创建的 MAC 地址。 |

 

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

 

 




