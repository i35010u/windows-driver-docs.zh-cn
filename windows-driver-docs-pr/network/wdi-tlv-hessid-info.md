---
title: WDI_TLV_HESSID_INFO
description: WDI_TLV_HESSID_INFO 是 TLV 包含 HESSID 信息，其中包括 HESSIDs、 访问网络类型和热点指示元素的列表。
ms.assetid: 60D130AC-8249-4B60-B46C-8B83FDDB148F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_HESSID_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 097f074b8be8f68614e6b760bb7e987d0f34fd5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546223"
---
# <a name="wditlvhessidinfo"></a>WDI\_TLV\_HESSID\_信息


WDI\_TLV\_HESSID\_信息是包含 HESSID 信息，其中包括一系列 HESSIDs、 访问网络类型和热点指示元素 TLV。

## <a name="tlv-type"></a>TLV 类型


0xFF

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                                                              |
|--------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ACCESS\_NETWORK\_TYPE**](wdi-tlv-access-network-type.md)               |                                |          | 若要在探测请求中使用的连接到的网络访问网络类型。 |
| [**WDI\_TLV\_HESSID**](wdi-tlv-hessid.md)                                           |                                |          | 端口允许连接到的 HESSIDs 的列表。                              |
| [**WDI\_TLV\_热点\_指示\_元素**](wdi-tlv-hotspot-indication-element.md) |                                |          | 要关联请求中使用的热点指示元素。                    |

 

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

 

 




