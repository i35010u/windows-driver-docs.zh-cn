---
title: WDI_TLV_CREATE_PORT_MAC_ADDRESS
description: WDI_TLV_CREATE_PORT_MAC_ADDRESS 是包含一个 MAC 地址用于 OID_WDI_TASK_CREATE_PORT TLV。
ms.assetid: CE2174E2-CFD7-40E7-B8A2-B96DDB6D6AA4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CREATE_PORT_MAC_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 06e99e197ea7d8733bea3db77feb7f65a6948d6c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348195"
---
# <a name="wditlvcreateportmacaddress"></a>WDI\_TLV\_创建\_端口\_MAC\_地址


WDI\_TLV\_创建\_端口\_MAC\_地址是包含的 MAC 地址 TLV [OID\_WDI\_任务\_创建\_端口](https://msdn.microsoft.com/library/windows/hardware/dn925949)。

## <a name="tlv-type"></a>TLV 类型


0xD9

## <a name="length"></a>长度


大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://msdn.microsoft.com/library/windows/hardware/dn926071)结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                   |
|---------------------------------------------------|-----------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 要使用的端口创建的 MAC 地址。 |

 

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

 

 




