---
title: HS_HOST_POST_CONNECT_AUTH_COMPLETION 函数
description: HS_HOST_POST_CONNECT_AUTH_COMPLETION 函数指示在第2层 Wi-fi 连接设置后的身份验证尝试是成功还是失败。
ms.assetid: 2c69802b-968b-400c-b02c-c2d39fa51d5a
keywords:
- typedef DWORD (WINAPI HS_HOST_POST_CONNECT_AUTH_COMPLETION 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8841bd4842a427fe2ea8c99cb96cec5e5f99e48f
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403094"
---
# <a name="hs_host_post_connect_auth_completion-function"></a>HS \_ 主机 \_ 后 \_ 连接 \_ 身份验证 \_ 完成功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 主机 \_ 后 \_ 连接 \_ 身份验证 \_ 完成**功能指示在第2层的 wi-fi 连接设置之后的身份验证尝试是成功还是失败。

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

<a name="parameters"></a>参数
----------

*hPluginContext* \[中\]  
调用此函数的插件的上下文句柄。

*dwConnectionId* \[中\]  
网络连接的唯一标识符。

*AuthResult* \[中\]  
[**EHS \_ AUTHENTICATION \_ 结果**](ehs-authentication-result.md)枚举值，指示成功或失败。

*pvReserved* \[in，可选\]  
留待将来使用。

<a name="return-value"></a>返回值
------------

此函数由插件调用，以与主机通信并且不返回值。

<a name="remarks"></a>备注
-------

插件必须调用此函数，以通知主机对 HS 插件的先前调用的结果将 [** \_ \_ 启动 \_ \_ 连接 \_ 身份验证**](hs-plugin-start-post-connect-auth.md)。

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

## <a name="see-also"></a>另请参阅


[**eHS \_ AUTHENTICATION \_ 结果**](ehs-authentication-result.md)

[**HS \_ 插件 \_ 启动 \_ 后 \_ 连接 \_ 身份验证**](hs-plugin-start-post-connect-auth.md)

 

 




