---
title: WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS 是包含关联响应结果参数的 TLV。
ms.assetid: 8BF2C8B4-207E-479A-9903-3FCDEED5BA2C
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 875d7bb4f0677db391d146c8069e5b123a2f32fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842882"
---
# <a name="wdi_tlv_association_response_result_parameters"></a>WDI\_TLV\_关联\_响应\_结果\_参数


WDI\_TLV\_ASSOCIATION\_响应\_结果\_参数是包含关联响应结果参数的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x76

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)"><strong>WDI_MAC_ADDRESS</strong></a></td>
<td>对等适配器的 MAC 地址。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>一个位值，该值指示对等工作站发出的请求是否为重新关联请求。
<p>有效值为0和1。 如果值为1，则表示它是一个重新关联请求。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>一个位值，该值指示对等工作站的响应是否为重新关联响应。
<p>有效值为0和1。 如果值为1，则表示它是重新关联响应。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm" data-raw-source="[&lt;strong&gt;WDI_AUTH_ALGORITHM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)"><strong>WDI_AUTH_ALGORITHM</strong></a></td>
<td>关联的身份验证算法。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)"><strong>WDI_CIPHER_ALGORITHM</strong></a></td>
<td>关联的单播密码算法。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)"><strong>WDI_CIPHER_ALGORITHM</strong></a></td>
<td>关联的多路广播密码算法。</td>
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
<td><p>Windows 10</p></td>
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

 

 




