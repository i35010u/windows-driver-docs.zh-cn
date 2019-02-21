---
title: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO
description: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO 是 TLV，其中包含有关传入关联请求的信息。
ms.assetid: E36ADD95-1751-4FCE-9032-900968878DEE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 95889b682cf985c926f7d0237be439e52fc960a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524037"
---
# <a name="wditlvincomingassociationrequestinfo"></a>WDI\_TLV\_传入\_关联\_请求\_信息


WDI\_TLV\_传入\_关联\_请求\_信息是 TLV，其中包含有关传入关联请求的信息。

## <a name="tlv-type"></a>TLV 类型


0x8F

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                            | 允许多个 TLV 实例 | 可选 | 描述                                                      |
|-----------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------|
| [**WDI\_TLV\_传入\_关联\_请求\_参数**](wdi-tlv-incoming-association-request-parameters.md) |                                |          | 传入关联请求的参数。             |
| [**WDI\_TLV\_ASSOCIATION\_REQUEST\_FRAME**](wdi-tlv-association-request-frame.md)                              |                                |          | 关联请求帧。                                   |
| [**WDI\_TLV\_ASSOCIATION\_REQUEST\_DEVICE\_CONTEXT**](wdi-tlv-association-request-device-context.md)           |                                | X        | 向下传递到该端口的特定于供应商的信息。 |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




