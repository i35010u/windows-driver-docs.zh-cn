---
title: WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE
description: WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE 是包含请求的关联参数 TLV 类型 TLV。
ms.assetid: BF4FE327-56A6-4EEE-B6C2-9B93D5C1DD47
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6fab91a66e56360eb20c880dfd2482528498bdd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568954"
---
# <a name="wditlvassociationparametersrequestedtype"></a>WDI\_TLV\_关联\_参数\_请求\_类型


WDI\_TLV\_关联\_参数\_请求\_类型是包含请求的关联参数 TLV 类型 TLV。

## <a name="tlv-type"></a>TLV 类型


0xBB

## <a name="length"></a>长度


UINT16 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入       | 描述                                                                                                                                                                                                                                  |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16\[\] | 请求的关联参数 TLV 类型的列表。 有效 TLV 类型为[ **WDI\_TLV\_PMKID** ](wdi-tlv-pmkid.md) (0x9F) 和[ **WDI\_TLV\_额外\_关联\_请求\_IES** ](wdi-tlv-extra-association-request-ies.md) (0x40)。 |

 

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

 

 




