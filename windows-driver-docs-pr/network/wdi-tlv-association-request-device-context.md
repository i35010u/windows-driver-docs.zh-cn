---
title: WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT
description: WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT 是一种 TLV，其中包含特定于供应商的信息，当主机决定向传入关联请求发送响应时，这些信息将向下传递到端口。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 66a92f6b78fb463772bcf3da75d1abd933b24d78
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808571"
---
# <a name="wdi_tlv_association_request_device_context"></a>WDI \_ TLV \_ 关联 \_ 请求 \_ 设备 \_ 上下文


WDI \_ tlv \_ 关联 \_ 请求 \_ 设备 \_ 上下文是一个 TLV，其中包含特定于供应商的信息，当主机决定向传入关联请求发送响应时向下传递到该端口。

## <a name="tlv-type"></a>TLV 类型


0x72

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                                           |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 当主机决定向传入关联请求发送响应时，向下传递到端口的供应商特定信息。 |

 

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

 

 




