---
title: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST
description: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST 是 TLV 包含 Wi-Fi Direct 接口的地址列表。
ms.assetid: B7FCB047-28D2-43E2-B4D6-B24E7BC74D47
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INTERFACE_ADDRESS_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c5bfbd8b5f56b3b329aeaaae9540cb1c6bcc47ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347259"
---
# <a name="wditlvp2pinterfaceaddresslist"></a>WDI\_TLV\_P2P\_INTERFACE\_ADDRESS\_LIST


WDI\_TLV\_P2P\_界面\_地址\_列表是包含 Wi-Fi Direct 接口的地址列表 TLV。

## <a name="tlv-type"></a>TLV 类型


0x18

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://msdn.microsoft.com/library/windows/hardware/dn926071)结构。 该数组必须包含一个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                  | 描述                      |
|-------------------------------------------------------|----------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071)\[\] | Wi-fi MAC 地址的数组。 |

 

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

 

 




