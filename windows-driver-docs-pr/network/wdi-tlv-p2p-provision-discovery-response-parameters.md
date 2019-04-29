---
title: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_PARAMETERS 是 TLV，其中包含预配发现响应参数。
ms.assetid: 0732C370-108E-4C9A-AF13-2B7D54AEB984
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 390728f8d9d58ac0e209a3cca45ec5621bfa3f9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362901"
---
# <a name="wditlvp2pprovisiondiscoveryresponseparameters"></a>WDI\_TLV\_P2P\_预配\_发现\_响应\_参数


WDI\_TLV\_P2P\_预配\_发现\_响应\_参数是包含预配发现响应参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x113

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                                                                           |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | Wi-Fi Direct 组功能位掩码。 位掩码相匹配的 Wi-fi P2P 技术规范的表 13 组功能位图定义中定义。 |
| UINT8 | 通过上述的组功能位图中的操作系统设置的位数。                                                                                            |

 

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

 

 




