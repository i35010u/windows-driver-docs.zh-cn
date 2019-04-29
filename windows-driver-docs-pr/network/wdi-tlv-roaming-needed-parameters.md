---
title: WDI_TLV_ROAMING_NEEDED_PARAMETERS
description: WDI_TLV_ROAMING_NEEDED_PARAMETERS 是 TLV 包含漫游触发器的原因。 这是 NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED 负载中使用。
ms.assetid: 152F923C-ECAE-4D50-A7B4-4B2309D5A3B5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ROAMING_NEEDED_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f1d14aa9cf18d423bbdf99dd86ba7a6cc87bd907
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359366"
---
# <a name="wditlvroamingneededparameters"></a>WDI\_TLV\_ROAMING\_NEEDED\_PARAMETERS


WDI\_TLV\_漫游\_需执行\_参数是包含漫游触发器的原因 TLV。 使用此[NDIS\_状态\_WDI\_指示\_漫游\_需执行](https://msdn.microsoft.com/library/windows/hardware/dn925648)有效负载。

## <a name="tlv-type"></a>TLV 类型


0x55

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                | 描述                                                                                                                                      |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ASSOC\_状态**](https://msdn.microsoft.com/library/windows/hardware/dn897725) | 指定漫游触发器的原因。 当[OID\_WDI\_任务\_漫游](https://msdn.microsoft.com/library/windows/hardware/dn925958)是触发，因此转发给它。 |

 

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

 

 




