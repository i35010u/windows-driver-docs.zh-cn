---
title: WDI_TLV_CONNECTION_SETTINGS
description: WDI_TLV_CONNECTION_SETTINGS 是包含连接设置 OID_WDI_TASK_CONNECT TLV。
ms.assetid: E08E895D-BFD6-496E-82FE-881FDDB0B88E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECTION_SETTINGS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 99d814d05a4e8569e2a99d86ae1021f4a24ff8b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357255"
---
# <a name="wditlvconnectionsettings"></a>WDI\_TLV\_连接\_设置


WDI\_TLV\_连接\_设置为包含的连接设置 TLV [OID\_WDI\_任务\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/dn925948)。

## <a name="tlv-type"></a>TLV 类型


0x3F

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                         | 描述                                                                                                                                                                                                               |
|--------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                                        | 指定是否这是首次连接请求 （值为 0） 或漫游连接 （值为 1）。                                                                                                                   |
| UINT8                                                        | 指定这是否与使用隐藏/非广播 Ssid 网络的连接。 连接到隐藏网络时，此值为 1。                                                                                      |
| UINT8                                                        | 这会设置 dot11ExcludeUnencrypted MIB。 当此值为 false (0) 和密码算法是 WEP，必须连接到未在管理帧中设置隐私字段的 Ap 的端口。                             |
| UINT8                                                        | 指定 MFP 是否已启用 (1) 还是禁用 (0)。 工作站必须播发其 802.11w 关联中的功能请求，当且仅当此值设置为 1 （启用）。                                          |
| UINT8                                                        | 指定主机 FIPS 模式下是否已启用 (1) 还是禁用 (0)。                                                                                                                                                               |
| [**WDI\_ASSOC\_状态**](https://msdn.microsoft.com/library/windows/hardware/dn897725) (UINT32) | 指定所需的漫游原因。 如果这由于触发[NDIS\_状态\_WDI\_指示\_漫游\_需执行](https://msdn.microsoft.com/library/windows/hardware/dn925648)，其中包含从漫游指示的原因。 |
| [**WDI\_ROAM\_TRIGGER**](https://msdn.microsoft.com/library/windows/hardware/mt269103) (UINT32) | 指定此漫游是关键漫游因为 AP 已设置其 BSS 转换请求操作框架中解除关联即将位。                                                                         |
| UINT8                                                        | 指定如果 802.11v BSS 转换支持。 如果此位设置为 1，工作站必须设置为 1 关联请求中的扩展功能元素 (位 19) 的 BSS 转换字段。                   |

 

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

 

 




