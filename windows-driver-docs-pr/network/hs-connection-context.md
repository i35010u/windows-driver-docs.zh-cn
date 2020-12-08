---
title: HS_CONNECTION_CONTEXT 结构
description: HS_CONNECTION_CONTEXT 结构包含插件用于 post 连接身份验证所需的信息。
keywords:
- 从 Windows Vista 开始 HS_CONNECTION_CONTEXT 结构网络驱动程序
- 从 Windows Vista 开始 PHS_CONNECTION_CONTEXT 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ed8b120f2e6ca77e80b4b6881e6aab96dc553ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814207"
---
# <a name="hs_connection_context-structure"></a>HS \_ 连接 \_ 上下文结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 连接 \_ 上下文** 结构包含插件用于 post 连接身份验证所需的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_CONNECTION_CONTEXT {
  HS_MAC_ADDRESS  MacAddress;
  HS_SIM_IDENTITY SIMIdentity;
  WCHAR           pszPhoneNumber[HS_MAX_PHONE_NUMBER_LENGTH+1];
} HS_CONNECTION_CONTEXT, *PHS_CONNECTION_CONTEXT;
```

<a name="members"></a>成员
-------

**MacAddress**  
包含 MAC 地址的 [**HS \_ mac \_ 地址**](hs-mac-address.md) 结构。

**SIMIdentity**  
[**HS \_ sim \_ 标识**](hs-sim-identity.md)结构，其中包含 EAP-SIM/称为身份验证所需的信息。

**pszPhoneNumber**  
指向电话号码的指针。

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

## <a name="see-also"></a>请参阅


[**HS \_ MAC \_ 地址**](hs-mac-address.md)

[**HS \_ SIM \_ 标识**](hs-sim-identity.md)

 

 




