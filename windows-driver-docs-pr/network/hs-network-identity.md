---
title: HS_NETWORK_IDENTITY 结构
description: HS_NETWORK_IDENTITY 结构包含唯一标识的 Wi-fi 网络的信息。
ms.assetid: 40d9720b-c122-4d19-8907-cfa2a05014e7
keywords:
- HS_NETWORK_IDENTITY 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_NETWORK_IDENTITY 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9bbffa2b2b153be41a8443eb8cf74d1f0c1136b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351040"
---
# <a name="hsnetworkidentity-structure"></a>HS\_网络\_IDENTITY 结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_网络\_标识**结构包含唯一标识的 Wi-fi 网络的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_NETWORK_IDENTITY {
  HS_SSID             Ssid;
  HS_AUTH_ALGORITHM   hsAuthAlgo;
  HS_CIPHER_ALGORITHM hsCipherAlgo;
} HS_NETWORK_IDENTITY, *PHS_NETWORK_IDENTITY;
```

<a name="members"></a>成员
-------

**ssid**  
网络 SSID。

**hsAuthAlgo**  
使用无线网络的身份验证算法。

**hsCipherAlgo**  
无线网络所用的密码算法。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




