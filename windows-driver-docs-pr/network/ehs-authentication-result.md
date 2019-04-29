---
title: eHS_AUTHENTICATION_RESULT 枚举
description: EHS_AUTHENTICATION_RESULT 枚举指示 PostConnectAuth 请求后由插件的身份验证的结果。
ms.assetid: a61ddc7c-8df8-410c-83df-9058e88bce51
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 eHS_AUTHENTICATION_RESULT 枚举
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: e68b8ee341f7cdf903d16eccbff85d44baafe4d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372568"
---
# <a name="ehsauthenticationresult-enumeration"></a>eHS\_身份验证\_结果枚举

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**EHS\_身份验证\_结果**枚举 PostConnectAuth 请求后由插件指示身份验证的结果。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum _eHS_AUTHENTICATION_RESULT { 
  HS_AUTHENTICATION_RESULT_SUCCESS         = 0,
  HS_AUTHENTICATION_RESULT_FAILED_TIMEOUT  = 100,
  HS_AUTHENTICATION_RESULT_FAILED_AUTH,
  HS_AUTHENTICATION_RESULT_FAILED_CONNECT,
  HS_AUTHENTICATION_RESULT_FAILED_OTHER,
  HS_AUTHENTICATION_RESULT_MAX
} eHS_AUTHENTICATION_RESULT;
```

<a name="constants"></a>常量
---------

<a href="" id="hs-authentication-result-success"></a>**HS\_身份验证\_结果\_成功**  
指示身份验证成功。

<a href="" id="hs-authentication-result-failed-timeout"></a>**HS\_身份验证\_结果\_失败\_超时**  
指示身份验证失败，因为从 server/后端超时。

<a href="" id="hs-authentication-result-failed-auth"></a>**HS\_身份验证\_结果\_失败\_身份验证**  
指示身份验证失败，因为不正确的凭据。

<a href="" id="hs-authentication-result-failed-connect"></a>**HS\_身份验证\_结果\_失败\_连接**  
指示身份验证失败，因为无法连接到身份验证服务器

<a href="" id="hs-authentication-result-failed-other"></a>**HS\_身份验证\_结果\_失败 \_ /伙伴**  
指示由于其他某种原因失败的身份验证。

<a href="" id="hs-authentication-result-max"></a>**HS\_身份验证\_结果\_最大值**  
指示一个范围外的值。

<a name="remarks"></a>备注
-------

该插件将此枚举值传递给热点插件宿主通过[ **HS\_主机\_POST\_CONNECT\_身份验证\_完成**](hs-host-post-connect-auth-completion.md)函数，用来通知调用的结果的热点插件主机[ **HS\_插件\_启动\_POST\_CONNECT\_身份验证**](hs-plugin-start-post-connect-auth.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




