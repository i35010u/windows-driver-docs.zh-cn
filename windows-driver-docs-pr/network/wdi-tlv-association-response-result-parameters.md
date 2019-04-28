---
title: WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS 是 TLV，其中包含关联响应结果参数。
ms.assetid: 8BF2C8B4-207E-479A-9903-3FCDEED5BA2C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8278c7e46002e0501a1c14073e46233f619335a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342268"
---
# <a name="wditlvassociationresponseresultparameters"></a>WDI\_TLV\_关联\_响应\_结果\_参数


WDI\_TLV\_关联\_响应\_结果\_参数是包含关联响应结果参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x76

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

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
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926071" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926071)"><strong>WDI_MAC_ADDRESS</strong></a></td>
<td>对等方适配器的 MAC 地址。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>一个位值，指示从对等方工作站请求是否重新关联请求。
<p>有效值为 0 和 1。 如果值为 1 指示这是一个重新关联请求。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>一个位值，指示来自对等方工作站的响应是否重新关联响应。
<p>有效值为 0 和 1。 如果值为 1 指示它是重新关联响应。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897792" data-raw-source="[&lt;strong&gt;WDI_AUTH_ALGORITHM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897792)"><strong>WDI_AUTH_ALGORITHM</strong></a></td>
<td>用于关联的身份验证算法。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897802" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897802)"><strong>WDI_CIPHER_ALGORITHM</strong></a></td>
<td>关联单播密码算法。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897802" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897802)"><strong>WDI_CIPHER_ALGORITHM</strong></a></td>
<td>用于关联的多播的密码算法。</td>
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




