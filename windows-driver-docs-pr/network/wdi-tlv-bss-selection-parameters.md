---
title: WDI_TLV_BSS_SELECTION_PARAMETERS
description: WDI_TLV_BSS_SELECTION_PARAMETERS 是包含由主机用于 BSS 选择 WDI_BSS_SELECTION_FLAGS TLV。
ms.assetid: 5EDA0FAC-DF2E-437B-BB4F-F69468CE856E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_SELECTION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b8d548a7aae8947970042925aeaf748f0a707425
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382617"
---
# <a name="wditlvbssselectionparameters"></a>WDI\_TLV\_BSS\_SELECTION\_PARAMETERS


WDI\_TLV\_BSS\_选择\_参数是包含 TLV [ **WDI\_BSS\_选择\_标志**](https://msdn.microsoft.com/library/windows/hardware/mt297629) BSS 选择使用由主机的。

## <a name="tlv-type"></a>TLV 类型


0x10F

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                     |
|--------|-----------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_BSS\_选择\_标志**](https://msdn.microsoft.com/library/windows/hardware/mt297629) ，用于主机 BSS 所选内容。 |

 

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

 

 




