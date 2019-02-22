---
title: HS_MAC_ADDRESS 结构
description: HS_MAC_ADDRESS 结构包含主机媒体访问控制 (MAC) 地址。
ms.assetid: 2d632ed4-4522-48ae-b23d-927517185d73
keywords:
- HS_MAC_ADDRESS 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_MAC_ADDRESS 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3da45d1c5f9088da55ec0b771ecfecc433b25ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525675"
---
# <a name="hsmacaddress-structure"></a>HS\_MAC\_地址结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_MAC\_地址**结构包含主机媒体访问控制 (MAC) 地址。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




