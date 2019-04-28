---
title: WDI_TLV_P2P_INSTANCE_NAME
description: WDI_TLV_P2P_INSTANCE_NAME 是包含该服务的实例名称 TLV。
ms.assetid: 36CB51E2-D8CB-4C71-B2DB-77F4FDBB8B90
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INSTANCE_NAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4d26711f00edc3d1cf677d0a2c3b5b765295d29f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347257"
---
# <a name="wditlvp2pinstancename"></a>WDI\_TLV\_P2P\_INSTANCE\_NAME


WDI\_TLV\_P2P\_实例\_名称是包含该服务的实例名称 TLV。

**请注意**  此 TLV 添加 Windows 10，版本 1607，WDI 版本 1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12B

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                     |
|-----------|-----------------------------------------------------------------|
| UINT8\[\] | 中-8，最多 63 个字节长的服务实例名称。 |

 

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

 

 




