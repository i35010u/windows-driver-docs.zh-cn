---
title: HS_HOST_POST_CONNECT_AUTH_COMPLETION 函数
description: HS_HOST_POST_CONNECT_AUTH_COMPLETION 函数指示成功或失败的身份验证尝试遵循在第 2 层的 Wi-fi 连接设置。
ms.assetid: 2c69802b-968b-400c-b02c-c2d39fa51d5a
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_HOST_POST_CONNECT_AUTH_COMPLETION) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e538fc9bbec138e7f7de0fae9117c2b1b00e5c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349643"
---
# <a name="hshostpostconnectauthcompletion-function"></a>HS\_主机\_POST\_CONNECT\_身份验证\_完成函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_主机\_POST\_CONNECT\_身份验证\_完成**函数指示成功或失败的身份验证尝试以下 Wi-fi 连接在第 2 层的安装程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_POST_CONNECT_AUTH_COMPLETION)(
  _In_     HANDLE                    hPluginContext,
  _In_     DWORD                     dwConnectionId,
  _In_     eHS_AUTHENTICATION_RESULT AuthResult,
  _In_opt_ LPVOID                    pvReserved
);
```

<a name="parameters"></a>Parameters
----------

*hPluginContext* \[in\]  
此函数在调用插件的上下文句柄。

*dwConnectionId* \[in\]  
网络连接的唯一标识符。

*AuthResult* \[in\]  
[ **EHS\_身份验证\_结果**](ehs-authentication-result.md)枚举值，该值指示成功或失败。

*pvReserved* \[in, optional\]  
保留供将来使用。

<a name="return-value"></a>返回值
------------

此函数调用由插件与主机通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

该插件必须调用此函数来通知以前调用的结果的宿主[ **HS\_插件\_启动\_POST\_CONNECT\_身份验证**](hs-plugin-start-post-connect-auth.md).

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

## <a name="see-also"></a>请参阅


[**eHS\_AUTHENTICATION\_RESULT**](ehs-authentication-result.md)

[**HS\_PLUGIN\_START\_POST\_CONNECT\_AUTH**](hs-plugin-start-post-connect-auth.md)

 

 




