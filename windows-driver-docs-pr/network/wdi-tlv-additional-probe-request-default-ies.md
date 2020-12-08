---
title: WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES
description: WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES 是一种 TLV，其中包含其他探测请求。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 770fc4288f7fe6dd7ccb2f2e829901831e8cd4fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822029"
---
# <a name="wdi_tlv_additional_probe_request_default_ies"></a>WDI \_ TLV \_ 附加 \_ 探测 \_ 请求 \_ 默认值 \_


WDI \_ tlv 的 \_ 其他 \_ 探测 \_ 请求 \_ 默认 \_ 为一个 tlv，其中包含其他探测请求。

## <a name="tlv-type"></a>TLV 类型


0x70

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8 []</td>
<td>发出探测请求的数组。 Wi-Fi 直接端口必须向传输的探测请求数据包添加这些附加的。
<div class="alert">
<strong>注意</strong>  Wi-Fi 的直接发现请求可能会覆盖默认的探测请求。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

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

 

 




