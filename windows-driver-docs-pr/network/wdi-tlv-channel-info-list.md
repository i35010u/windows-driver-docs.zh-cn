---
title: WDI_TLV_CHANNEL_INFO_LIST
description: WDI_TLV_CHANNEL_INFO_LIST 是包含一系列通道 TLV。
ms.assetid: D1B82F4F-6722-4D54-B6FF-B7F1309F8C0E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHANNEL_INFO_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7bfd6f2954c03c795c2e64eb8ae1a62fccaa8cfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526405"
---
# <a name="wditlvchannelinfolist"></a>WDI\_TLV\_通道\_信息\_列表


WDI\_TLV\_通道\_信息\_列表是包含一系列通道 TLV。

## <a name="tlv-type"></a>TLV 类型


0x41

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_通道\_数 (UINT32) 结构。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入       | 描述                 |
|------------|-----------------------------|
| UINT32\[\] | Wi-fi 信道的数组。 |

 

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

 

 




