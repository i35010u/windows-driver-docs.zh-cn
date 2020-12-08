---
title: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO
description: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO 是一种 TLV，其中包含传入关联请求的相关信息。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 452dd5a96c5fc4c49ee59e76fe7e74b54838e696
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837095"
---
# <a name="wdi_tlv_incoming_association_request_info"></a>WDI \_ TLV \_ 传入 \_ 关联 \_ 请求 \_ 信息


WDI \_ tlv \_ 传入 \_ 关联 \_ 请求 \_ 信息是一个 tlv，其中包含传入关联请求的相关信息。

## <a name="tlv-type"></a>TLV 类型


0x8F

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                            | 允许多个 TLV 实例 | 可选 | 说明                                                      |
|-----------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------|
| [**WDI \_ TLV \_ 传入 \_ 关联 \_ 请求 \_ 参数**](wdi-tlv-incoming-association-request-parameters.md) |                                |          | 传入关联请求的参数。             |
| [**WDI \_ TLV \_ 关联 \_ 请求 \_ 帧**](wdi-tlv-association-request-frame.md)                              |                                |          | 关联请求框架。                                   |
| [**WDI \_ TLV \_ 关联 \_ 请求 \_ 设备 \_ 上下文**](wdi-tlv-association-request-device-context.md)           |                                | X        | 向下传递到端口的供应商特定信息。 |

 

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

 

 




