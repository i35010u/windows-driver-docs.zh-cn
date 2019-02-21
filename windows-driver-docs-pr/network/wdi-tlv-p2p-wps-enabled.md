---
title: WDI_TLV_P2P_WPS_ENABLED
description: WDI_TLV_P2P_WPS_ENABLED 是 TLV，指定是否启用了 Wi-fi 受保护的安装程序。
ms.assetid: B923DA17-451C-4BF1-8B8B-C2846EDE9774
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_WPS_ENABLED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 54b3405d2bda5fa6da023aa66e3bedec20930374
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543535"
---
# <a name="wditlvp2pwpsenabled"></a>WDI\_TLV\_P2P\_WPS\_ENABLED


WDI\_TLV\_P2P\_WPS\_已启用是 TLV，指定是否启用了 Wi-fi 受保护的安装程序。

## <a name="tlv-type"></a>TLV 类型


0xF7

## <a name="length"></a>长度


超出 UINT8 的大小 （以字节为单位）。

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
<td>UINT8</td>
<td>指定是否启用了 Wi-fi 受保护的安装程序。
<p>有效值为 0 （未启用） 和 1 （启用）。</p></td>
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

## <a name="see-also"></a>另请参阅


[OID\_WDI\_SET\_P2P\_WPS\_ENABLED](https://msdn.microsoft.com/library/windows/hardware/dn925938)

 

 




