---
title: HS_NETWORK_IDENTITY 结构
description: HS_NETWORK_IDENTITY 结构包含唯一标识 Wi-Fi 网络的信息。
keywords:
- 从 Windows Vista 开始 HS_NETWORK_IDENTITY 结构网络驱动程序
- 从 Windows Vista 开始 PHS_NETWORK_IDENTITY 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb38e6b3898bdfaee4a3507cd7a28676715e17d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814157"
---
# <a name="hs_network_identity-structure"></a>HS \_ 网络 \_ 标识结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 网络 \_ 标识** 结构包含唯一标识 Wi-Fi 网络的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_NETWORK_IDENTITY {
  HS_SSID             Ssid;
  HS_AUTH_ALGORITHM   hsAuthAlgo;
  HS_CIPHER_ALGORITHM hsCipherAlgo;
} HS_NETWORK_IDENTITY, *PHS_NETWORK_IDENTITY;
```

<a name="members"></a>成员
-------

**Ssid**  
网络 SSID。

**hsAuthAlgo**  
无线网络使用的身份验证算法。

**hsCipherAlgo**  
无线网络使用的密码算法。

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

 

 




