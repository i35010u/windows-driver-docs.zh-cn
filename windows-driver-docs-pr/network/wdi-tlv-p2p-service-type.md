---
title: WDI_TLV_P2P_SERVICE_TYPE
description: WDI_TLV_P2P_SERVICE_TYPE 是包含该服务的服务类型 TLV。
ms.assetid: D9C3F099-DED1-400E-9D3F-7AF6D2D286DF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_TYPE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4fd6f6ffbdeefe833d7c2c502b03e32019127601
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519546"
---
# <a name="wditlvp2pservicetype"></a>WDI\_TLV\_P2P\_SERVICE\_TYPE


WDI\_TLV\_P2P\_服务\_类型是包含该服务的服务类型 TLV。

**请注意**  此 TLV 添加 Windows 10，版本 1607，WDI 版本 1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x129

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                    |
|-----------|----------------------------------------------------------------|
| UINT8\[\] | UTF-8，最多 21 个字节中服务的服务类型。 |

 

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

 

 




