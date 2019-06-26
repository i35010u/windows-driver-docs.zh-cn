---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_GET
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_GET 是包含一种协议 TLV 卸载 OID_WDI_GET_PM_PROTOCOL_OFFLOAD 的 ID。
ms.assetid: 71BBAA8F-0EE3-4315-AEB1-E9FD394218AD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_GET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3c8cd3d48be2bdb5a0e08ce56689c1737474fffd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373853"
---
# <a name="wditlvpmprotocoloffloadget"></a>WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_GET


WDI\_TLV\_PM\_协议\_卸载\_GET 是包含的协议卸载 ID TLV [OID\_WDI\_获取\_PM\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-pm-protocol-offload)。

## <a name="tlv-type"></a>TLV 类型


0xA8

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                                                                                                                                                 |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 指定协议卸载 id。 这是一个操作系统提供的值，标识已卸载的协议。 操作系统向下发送添加请求或对基础驱动程序的请求完成之前，为在协议中唯一值的 OS 集 ProtocolOffloadId 将卸载网络适配器上。 |

 

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

 

 




