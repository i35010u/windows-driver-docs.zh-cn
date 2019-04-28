---
title: WDI_TLV_SUPPORTED_GUIDS
description: WDI_TLV_SUPPORTED_GUIDS 是包含受支持的 NDIS GUID TLV。
ms.assetid: 957645EE-A6E3-402E-B18B-B2E7C73D6F6B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SUPPORTED_GUIDS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cd7980524d3fd6716a3968eeecdabeac6d44293e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330433"
---
# <a name="wditlvsupportedguids"></a>WDI\_TLV\_支持\_GUID


WDI\_TLV\_支持\_GUID 是包含受支持的 NDIS GUID TLV。

**请注意**  此 TLV 添加 Windows 10，版本 1607，WDI 版本 1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x130

## <a name="length"></a>长度


大小 （以字节为单位） [NDIS\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff549898)结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入       | 描述            |
|------------|------------------------|
| NDIS\_GUID | 支持的 NDIS GUID。 |

 

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

## <a name="see-also"></a>请参阅


[OID\_WDI\_获取\_适配器\_功能](https://msdn.microsoft.com/library/windows/hardware/dn925838)

 

 




