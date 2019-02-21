---
title: WDI_TLV_P2P_DEVICE_NAME
description: WDI_TLV_P2P_DEVICE_NAME 是 TLV 包含设备名称。
ms.assetid: 7FB04079-7F82-4D7B-95BA-45B5832B36C0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_NAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ddf8dc3c5803ff805b49d3b36b8a656c25f4cce7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526166"
---
# <a name="wditlvp2pdevicename"></a>WDI\_TLV\_P2P\_DEVICE\_NAME


WDI\_TLV\_P2P\_设备\_名称是包含设备名称 TLV。

## <a name="tlv-type"></a>TLV 类型


0x92

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                               |
|-----------|---------------------------------------------------------------------------|
| UINT8\[\] | 指定设备的设备名称 UINT8 元素的数组。 |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




