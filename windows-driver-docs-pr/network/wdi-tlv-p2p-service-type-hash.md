---
title: WDI_TLV_P2P_SERVICE_TYPE_HASH
description: WDI_TLV_P2P_SERVICE_TYPE_HASH 是包含服务类型的哈希 TLV。
ms.assetid: A475C2E3-F558-47EC-9708-87887AE2D8AF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_TYPE_HASH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f7d917821f5f4a01ac3903a48bb4d337820cd188
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375641"
---
# <a name="wditlvp2pservicetypehash"></a>WDI\_TLV\_P2P\_SERVICE\_TYPE\_HASH


WDI\_TLV\_P2P\_服务\_类型\_哈希是包含服务类型的哈希 TLV。

**请注意**  此 TLV 添加 Windows 10，版本 1607，WDI 版本 1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12A

## <a name="length"></a>长度


大小 （以字节为单位） [ **WDI\_P2P\_服务\_名称\_哈希**](https://msdn.microsoft.com/library/windows/hardware/dn926103)结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述               |
|-------------------------------------------------------------------------|---------------------------|
| [**WDI\_P2P\_SERVICE\_NAME\_HASH**](https://msdn.microsoft.com/library/windows/hardware/dn926103) | 服务类型的哈希值。 |

 

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

 

 




