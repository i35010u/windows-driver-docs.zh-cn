---
title: HS_MAC_ADDRESS 结构
description: HS_MAC_ADDRESS 结构包含 (MAC) 地址的主机媒体访问控制。
keywords:
- 从 Windows Vista 开始 HS_MAC_ADDRESS 结构网络驱动程序
- 从 Windows Vista 开始 PHS_MAC_ADDRESS 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1ba07721e6e1556ceff8a3b6099baec06649ccb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814161"
---
# <a name="hs_mac_address-structure"></a>HS \_ MAC \_ 地址结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ mac \_ 地址** 结构包含主机媒体访问控制 (MAC) 地址。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_MAC_ADDRESS {
  UCHAR ucHSMacAddress[6];
} HS_MAC_ADDRESS, *PHS_MAC_ADDRESS;
```

<a name="members"></a>成员
-------

**ucHSMacAddress**  
MAC 地址。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




