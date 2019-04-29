---
title: HS_PLUGIN_START_POST_CONNECT_AUTH 函数
description: 调用 HS_PLUGIN_START_POST_CONNECT_AUTH 函数来执行任何后续连接设备通过网络进行身份验证所需的身份验证。
ms.assetid: f52236fc-2afd-46e2-ae88-7c4fa10f8d59
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_START_POST_CONNECT_AUTH) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeeecb7294e73222600df3762addb7b36ed55ce8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322166"
---
# <a name="hspluginstartpostconnectauth-function"></a>HS\_插件\_启动\_POST\_CONNECT\_身份验证函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_启动\_POST\_CONNECT\_身份验证**调用函数来执行任何后续连接对设备进行身份验证所需的身份验证在网络中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_START_POST_CONNECT_AUTH)(
  _In_ DWORD                 dwConnectionId,
  _In_ HS_CONNECTION_CONTEXT *pConnectContext,
  _In_ HS_SIM_DATA           *pSIMData,
  _In_ HS_NETWORK_IDENTITY   *pNetworkIdentity,
  _In_ HS_NETWORK_PROFILE    *pNetworkProfile
);
```

<a name="parameters"></a>Parameters
----------

*dwConnectionId* \[in\]  
网络连接的唯一标识符。

*\*pConnectContext* \[in\]  
指向[ **HS\_连接\_上下文**](hs-connection-context.md)结构，其中包含适用于的插件所需的信息后连接身份验证。

*\*pSIMData* \[in\]  
指向[ **HS\_SIM\_数据**](hs-sim-data.md)结构，其中包含所需的适用于的插件 SIM 中的信息后连接身份验证。

*\*pNetworkIdentity* \[in\]  
指向[ **HS\_网络\_标识**](hs-network-identity.md)网络的结构。

*\*pNetworkProfile* \[in\]  
指向[ **HS\_网络\_配置文件**](hs-network-profile.md)结构，其中包含的网络配置文件。

<a name="return-value"></a>返回值
------------

此函数调用由宿主与插件进行通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

后调用此函数时，该插件必须调用[ **HS\_主机\_POST\_CONNECT\_身份验证\_完成**](hs-host-post-connect-auth-completion.md)到处理程序通知的主机的请求的状态。

如果网络使用也称为 EAP-SIM 身份验证，该插件不需要在此状态下执行任何活动。 但是，如果网络需要基于 HTTP 的身份验证，该插件必须执行相应的身份验证。

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


[**HS\_连接\_上下文**](hs-connection-context.md)

[**HS\_SIM\_DATA**](hs-sim-data.md)

[**HS\_NETWORK\_IDENTITY**](hs-network-identity.md)

[**HS\_NETWORK\_PROFILE**](hs-network-profile.md)

 

 




