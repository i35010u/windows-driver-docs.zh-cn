---
title: WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST
description: WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST 是 TLV 包含多播的数据算法对的数组。
ms.assetid: BF07170E-CF4E-4E93-85E1-3276E414BDD9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: df588cf19d381e39a1bf5da5d404efbe59dba84a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376999"
---
# <a name="wditlvmulticastdataalgorithmlist"></a>WDI\_TLV\_多播\_数据\_算法\_列表


WDI\_TLV\_多播\_数据\_算法\_列表是包含的多路广播的数据算法对数组 TLV。

## <a name="tlv-type"></a>TLV 类型


0x14

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_ALGO\_对元素。 该数组必须包含一个或多个元素。

**请注意**  WDI\_ALGO\_对不是 WDI 结构。 它定义在 WDI TLV 分析器生成器，并仅供文档使用。

 

## <a name="values"></a>值


| 在任务栏的搜索框中键入                 | 描述                                            |
|----------------------|--------------------------------------------------------|
| WDI\_ALGO\_PAIRS\[\] | 身份验证和加密算法对的数组。 |

 

WDI\_ALGO\_对以下元素组成。

| 在任务栏的搜索框中键入  | 描述                                                                                     |
|-------|-------------------------------------------------------------------------------------------------|
| UINT8 | 如中所定义的身份验证算法[ **WDI\_身份验证\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm)。 |
| UINT8 | 如中所定义的密码算法[ **WDI\_密码\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm)。     |

 

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

 

 




