---
title: WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR
description: WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR 是包含 Wi-Fi Direct 服务 TLV 更新指示器。
ms.assetid: C90579C9-55DD-4E32-BEA3-EB156F4A422C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 92ef75f7cf9906580a275229b12f60be30f7113d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566809"
---
# <a name="wditlvp2pserviceupdateindicator"></a>WDI\_TLV\_P2P\_SERVICE\_UPDATE\_INDICATOR


WDI\_TLV\_P2P\_服务\_更新\_指标是包含 Wi-Fi Direct 的服务更新指示器 TLV。

## <a name="tlv-type"></a>TLV 类型


0x115

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                 |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 要包括在 ANQP 响应中，如果该驱动程序支持对服务的信息发现 ANQP 请求的响应的服务更新指示器。 |

 

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

 

 




