---
title: WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES
description: WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES 是一种 TLV，其中包含必须包括在端口发送的关联请求中 () 的信息元素。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 332d058409f6aa93af6db2eb9205df531ac92d22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807963"
---
# <a name="wdi_tlv_extra_association_request_ies"></a>WDI \_ TLV \_ 额外 \_ 关联 \_ 请求 \_


WDI \_ tlv \_ 额外 \_ 关联 \_ 请求 \_ 是一个 tlv，其中包含必须包括在端口发送的关联请求) 中的信息 (元素。

## <a name="tlv-type"></a>TLV 类型


0x40

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                                                                                                                                                               |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素的数组，其中包含由端口发送的关联请求中必须包含的请求。 它们适用于设备关联的所有 BSSID。 除了常见的和 BSSID 的特定情况外，还应使用它们。 |

 

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

 

 




