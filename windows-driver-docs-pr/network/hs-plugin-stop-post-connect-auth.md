---
title: HS_PLUGIN_STOP_POST_CONNECT_AUTH 函数
description: HS_PLUGIN_STOP_POST_CONNECT_AUTH 函数调用以通知插件以停止身份验证过程。
ms.assetid: 2e4e01b1-e41a-41db-a3ca-6cc6b53b3a8b
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_STOP_POST_CONNECT_AUTH) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe1b3d25b236a1ae7a6afe43b30d3f9270b24649
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322165"
---
# <a name="hspluginstoppostconnectauth-function"></a>HS\_插件\_停止\_POST\_CONNECT\_身份验证函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_停止\_POST\_CONNECT\_身份验证**函数调用以通知插件以停止身份验证过程。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_STOP_POST_CONNECT_AUTH)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>Parameters
----------

*\*pNetworkIdentity* \[in\]  
[ **HS\_网络\_标识**](hs-network-identity.md)唯一标识网络的结构。

<a name="return-value"></a>返回值
------------

此函数调用由宿主与插件进行通信，并不会返回一个值。

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


[**HS\_NETWORK\_IDENTITY**](hs-network-identity.md)

 

 




