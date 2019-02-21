---
title: WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES
description: WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES 是包含其他探测请求导致浏览器 TLV。
ms.assetid: E364B1BC-5A78-42C8-B04D-31BD21141477
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4c6c46ce66ae9a393438fdf96f8e43c2e468cc35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544096"
---
# <a name="wditlvadditionalproberequestdefaulties"></a>WDI\_TLV\_ADDITIONAL\_PROBE\_REQUEST\_DEFAULT\_IES


WDI\_TLV\_其他\_探测\_请求\_默认\_导致浏览器是包含其他探测请求导致浏览器 TLV。

## <a name="tlv-type"></a>TLV 类型


0x70

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

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
<td>UINT8[]</td>
<td>探测请求导致浏览器的数组。 Wi-Fi Direct 端口必须将这些附加导致浏览器添加到传输的探测请求数据包。
<div class="alert">
<strong>请注意</strong>  Wi-Fi Direct 发现请求可能会重写默认探测请求导致浏览器。
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




