---
title: WDI_TLV_FT_REASSOC_PARAMETERS
description: WDI_TLV_FT_REASSOC_PARAMETERS 是一种 TLV，其中包含用于快速转换的重新关联参数。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_REASSOC_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3f03dec05303804159652a9570ad0815f90fda23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825375"
---
# <a name="wdi_tlv_ft_reassoc_parameters"></a>WDI \_ TLV \_ FT \_ REASSOC \_ 参数


WDI \_ tlv \_ FT \_ REASSOC \_ 参数是一个 tlv，其中包含用于快速转换的重新关联参数。

## <a name="tlv-type"></a>TLV 类型


0x106

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                    | 描述                                                                                                                            |
|---------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ FT \_ MDE**](wdi-tlv-ft-mde.md)             | BSS 项的 MDIE。                                                                                                             |
| [**WDI \_ TLV \_ FT \_ PMKR0NAME**](wdi-tlv-ft-pmkr0name.md) | PMKR0Name。 这是快速转换期间所需要的。 STA 需要在身份验证请求期间将 PMKR0Name 发送到 AP。 |
| [**WDI \_ TLV \_ FT \_ FTE**](wdi-tlv-ft-fte.md)             | 包含 R0KHID 和 SNonce 的快速转换元素。                                                                       |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




