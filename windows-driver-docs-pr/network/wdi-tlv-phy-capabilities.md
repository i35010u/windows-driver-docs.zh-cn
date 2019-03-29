---
title: WDI_TLV_PHY_CAPABILITIES
description: WDI_TLV_PHY_CAPABILITIES 是包含物理功能 TLV。
ms.assetid: 8F482ED6-6594-4DB5-B53B-4424DAD32D36
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 45426b6e8174a382807e04c71d10097f37bb0e3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563479"
---
# <a name="wditlvphycapabilities"></a>WDI\_TLV\_PHY\_功能


WDI\_TLV\_PHY\_功能是包含物理功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0x1B

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                        | 描述                                        |
|---------------------------------------------|----------------------------------------------------|
| [**WDI\_PHY\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/dn926105) | 指定物理类型。                           |
| UINT8                                       | 指定物理支持 CF 轮询。 |
| UINT32                                      | 指定 MPDU 最大长度。                 |
| UINT32                                      | 指定操作的温度类。         |
| UINT32                                      | 指定天线多样性支持。           |

 

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

 

 




