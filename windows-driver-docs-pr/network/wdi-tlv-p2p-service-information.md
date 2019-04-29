---
title: WDI_TLV_P2P_SERVICE_INFORMATION
description: WDI_TLV_P2P_SERVICE_INFORMATION 是 TLV 包含 Wi-Fi Direct 服务信息。
ms.assetid: C377FA31-1D78-4087-A600-18F10D9022B6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_INFORMATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d5b182411c3c2ad30f29962b93df4431d2a799ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392874"
---
# <a name="wditlvp2pserviceinformation"></a>WDI\_TLV\_P2P\_服务\_信息


WDI\_TLV\_P2P\_服务\_信息是包含 Wi-Fi Direct 服务信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0xEE

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                              |
|-----------|------------------------------------------|
| UINT8\[\] | 服务的服务信息。 |

 

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

 

 




