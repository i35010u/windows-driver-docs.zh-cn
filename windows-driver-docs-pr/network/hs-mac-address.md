---
title: HS_MAC_ADDRESS 结构
description: HS_MAC_ADDRESS 结构包含 (MAC) 地址的主机媒体访问控制。
ms.assetid: 2d632ed4-4522-48ae-b23d-927517185d73
keywords:
- 从 Windows Vista 开始 HS_MAC_ADDRESS 结构网络驱动程序
- 从 Windows Vista 开始 PHS_MAC_ADDRESS 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56f76baec058a15f070de16523fde6145d546480
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403078"
---
# <a name="hs_mac_address-structure"></a>HS \_ MAC \_ 地址结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ mac \_ 地址**结构包含主机媒体访问控制 (MAC) 地址。

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
<td><p>Header</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




