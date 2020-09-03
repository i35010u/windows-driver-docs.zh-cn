---
title: eHS_AUTHENTICATION_RESULT 枚举
description: EHS_AUTHENTICATION_RESULT 枚举指示 PostConnectAuth 请求之后的插件进行身份验证的结果。
ms.assetid: a61ddc7c-8df8-410c-83df-9058e88bce51
keywords:
- 从 Windows Vista 开始 eHS_AUTHENTICATION_RESULT 枚举网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89afdf1fe01591b197954e8214dc36a7b2ffed0f
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403548"
---
# <a name="ehs_authentication_result-enumeration"></a>eHS \_ AUTHENTICATION \_ 结果枚举

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**EHS \_ authentication \_ 结果**枚举指示 PostConnectAuth 请求后的插件进行身份验证的结果。

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

<a href="" id="hs-authentication-result-success"></a>**HS \_ 身份验证 \_ 结果 \_ 成功**  
指示身份验证成功。

<a href="" id="hs-authentication-result-failed-timeout"></a>**HS \_ 身份验证 \_ 结果 \_ 失败 \_ 超时**  
指示身份验证由于服务器/后端超时而失败。

<a href="" id="hs-authentication-result-failed-auth"></a>**HS \_ 身份验证 \_ 结果 \_ 失败 \_ 身份验证**  
指示身份验证因凭据错误而失败。

<a href="" id="hs-authentication-result-failed-connect"></a>**HS \_ 身份 \_ 验证 \_ 结果 \_ 连接失败**  
指示由于无法连接到身份验证服务器而导致身份验证失败

<a href="" id="hs-authentication-result-failed-other"></a>**HS \_ 身份验证 \_ 结果 \_ 失败 \_**  
指示身份验证因其他原因而失败。

<a href="" id="hs-authentication-result-max"></a>**HS \_ 身份验证 \_ 结果 \_ 最大值**  
指示超出范围值。

<a name="remarks"></a>备注
-------

此插件通过 [**HS \_ host \_ CONNECT authentication \_ \_ \_ 完成**](hs-host-post-connect-auth-completion.md) 函数将此枚举值传递到热点插件主机，该函数用于通知热点插件对对 HS 插件的调用结果的 [** \_ \_ 启动 \_ 后 \_ 连接 \_ 身份验证**](hs-plugin-start-post-connect-auth.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




