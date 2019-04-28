---
title: WDI_TLV_FT_REASSOC_PARAMETERS
description: WDI_TLV_FT_REASSOC_PARAMETERS 是快速转换为包含重新关联参数 TLV。
ms.assetid: 36F260FF-E80A-4EFF-B009-B06446229470
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_REASSOC_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 68f27c22888b4c9c53a66217bfbad87648335c86
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329718"
---
# <a name="wditlvftreassocparameters"></a>WDI\_TLV\_FT\_REASSOC\_PARAMETERS


WDI\_TLV\_FT\_REASSOC\_参数是包含重新关联参数，以便快速转换 TLV。

## <a name="tlv-type"></a>TLV 类型


0x106

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                    | 描述                                                                                                                            |
|---------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_FT\_MDE**](wdi-tlv-ft-mde.md)             | BSS 条目的 MDIE。                                                                                                             |
| [**WDI\_TLV\_FT\_PMKR0NAME**](wdi-tlv-ft-pmkr0name.md) | PMKR0Name。 快速转换期间需要此项。 需要将 PMKR0Name 期间身份验证请求发送到 AP STA。 |
| [**WDI\_TLV\_FT\_FTE**](wdi-tlv-ft-fte.md)             | 快速转换包含的元素的 R0KHID 和 SNonce。                                                                       |

 

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

 

 




