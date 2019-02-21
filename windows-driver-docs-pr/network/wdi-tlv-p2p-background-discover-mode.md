---
title: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE
description: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE 是包含 Wi-Fi Direct 背景发现模式参数 TLV。
ms.assetid: 987DB282-A992-497F-98B5-0D3DD477B91C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 65e0f53561d89462b4da11b69e4268b1a0f1552b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554512"
---
# <a name="wditlvp2pbackgrounddiscovermode"></a>WDI\_TLV\_P2P\_背景\_DISCOVER\_模式


WDI\_TLV\_P2P\_背景\_DISCOVER\_模式是包含 Wi-Fi Direct 背景发现模式参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0xCE

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
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926093" data-raw-source="[&lt;strong&gt;WDI_P2P_DISCOVER_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926093)"><strong>WDI_P2P_DISCOVER_TYPE</strong></a></td>
<td>通过该端口执行发现的类型。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926101" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926101)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></td>
<td>通过该端口执行服务发现的类型。
<p>唯一有效的值为 WDI_P2P_SERVICE_DISCOVERY_TYPE_NO_SERVICE_DISCOVERY 和 WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_NAME_ONLY。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>设备的可见性超时。 指定用于报告设备条目的最大超时 （以毫秒为单位）。 这是必需的仅背景扫描。</td>
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

 

 




