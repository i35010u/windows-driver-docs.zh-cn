---
title: WDI_TLV_VIRTUALIZATION_CAPABILITIES
description: WDI_TLV_VIRTUALIZATION_CAPABILITIES 是包含虚拟化功能 TLV。
ms.assetid: D72E9984-7193-406C-8BA3-006E54400B30
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_VIRTUALIZATION_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e5b3fae800f2d84916ff8a4ea3ce408cbc9fd745
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376633"
---
# <a name="wditlvvirtualizationcapabilities"></a>WDI\_TLV\_虚拟化\_功能


WDI\_TLV\_虚拟化\_功能是包含虚拟化功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0x10

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                                                                                                                                       |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 支持 ExtSTA 端口数。                                                                                                                                                                                             |
| UINT8 | 受支持的 Wi-Fi Direct 组端口数。 此计数只应包括角色端口。 如果此值为非零值，则假定 Wi-Fi Direct 设备端口是否可用。                                               |
| UINT8 | 支持旧 ExtAP 端口数。                                                                                                                                                                                       |
| UINT8 | 支持同时亚太/WFD 组所有者的最大数目。                                                                                                                                                                 |
| UINT8 | 单独的渠道，设备可以在操作和维护同时数据连接的数目上限。 此限制不应包括临时多渠道操作，例如扫描和 Wi-Fi Direct 协商。 |
| UINT8 | 支持同时 STA/WFD 客户端的最大数量。                                                                                                                                                                     |

 

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

 

 




