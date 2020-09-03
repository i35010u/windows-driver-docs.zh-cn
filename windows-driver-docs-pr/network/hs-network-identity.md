---
title: HS_NETWORK_IDENTITY 结构
description: HS_NETWORK_IDENTITY 结构包含唯一标识 Wi-fi 网络的信息。
ms.assetid: 40d9720b-c122-4d19-8907-cfa2a05014e7
keywords:
- 从 Windows Vista 开始 HS_NETWORK_IDENTITY 结构网络驱动程序
- 从 Windows Vista 开始 PHS_NETWORK_IDENTITY 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17e3f381dd69a146ec68db788ed2319355de37c3
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403066"
---
# <a name="hs_network_identity-structure"></a>HS \_ 网络 \_ 标识结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 网络 \_ 标识**结构包含唯一标识 wi-fi 网络的信息。

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
<td><p>Header</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




