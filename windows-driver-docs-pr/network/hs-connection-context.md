---
title: HS_CONNECTION_CONTEXT 结构
description: HS_CONNECTION_CONTEXT 结构包含 post 连接身份验证，该插件所需的信息。
ms.assetid: 22b219fc-691b-4813-a523-a76de037e64d
keywords:
- HS_CONNECTION_CONTEXT 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_CONNECTION_CONTEXT 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fe42ada75739323a10c0cbc78e0975ff7276a0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522673"
---
# <a name="hsconnectioncontext-structure"></a>HS\_连接\_上下文结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_连接\_上下文**结构包含 post 连接身份验证，该插件所需的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_CONNECTION_CONTEXT {
  HS_MAC_ADDRESS  MacAddress;
  HS_SIM_IDENTITY SIMIdentity;
  WCHAR           pszPhoneNumber[HS_MAX_PHONE_NUMBER_LENGTH+1];
} HS_CONNECTION_CONTEXT, *PHS_CONNECTION_CONTEXT;
```

<a name="members"></a>成员
-------

**MacAddress**  
[ **HS\_MAC\_地址**](hs-mac-address.md)结构，其中包含的 MAC 地址。

**SIMIdentity**  
[ **HS\_SIM\_标识**](hs-sim-identity.md)结构，其中包含也称为 EAP-SIM 身份验证所需的信息。

**pszPhoneNumber**  
电话号码的指针。

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

## <a name="see-also"></a>另请参阅


[**HS\_MAC\_ADDRESS**](hs-mac-address.md)

[**HS\_SIM\_标识**](hs-sim-identity.md)

 

 




