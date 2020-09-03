---
title: HS_PLUGIN_START_POST_CONNECT_AUTH 函数
description: 调用 HS_PLUGIN_START_POST_CONNECT_AUTH 函数来执行任何需要的连接后身份验证，以通过网络对设备进行身份验证。
ms.assetid: f52236fc-2afd-46e2-ae88-7c4fa10f8d59
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_START_POST_CONNECT_AUTH 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51600a8658d7edc5f74bea8b731a8033ffa38e97
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402996"
---
# <a name="hs_plugin_start_post_connect_auth-function"></a>HS \_ 插件 \_ 启动 \_ 后 \_ 连接 \_ 身份验证功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件会 \_ 启动 \_ post \_ \_ AUTH**功能，以执行在网络上对设备进行身份验证所需的任何连接后身份验证。

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

<a name="parameters"></a>参数
----------

*dwConnectionId* \[中\]  
网络连接的唯一标识符。

* \* pConnectContext* \[\]  
指向一个 [**HS \_ 连接 \_ 上下文**](hs-connection-context.md) 结构的指针，该结构包含插件进行后连接身份验证所需的信息。

* \* pSIMData* \[\]  
一个指向 [**HS \_ sim \_ 数据**](hs-sim-data.md) 结构的指针，该数据包包含插件要求的 sim 中的信息，用于连接后身份验证。

* \* pNetworkIdentity* \[\]  
指向网络的 [**HS \_ 网络 \_ 标识**](hs-network-identity.md) 结构的指针。

* \* pNetworkProfile* \[\]  
指向包含网络配置文件的 [**HS \_ 网络 \_ 配置文件**](hs-network-profile.md) 结构的指针。

<a name="return-value"></a>返回值
------------

宿主调用此函数以与插件通信，而不返回值。

<a name="remarks"></a>备注
-------

调用此函数后，插件必须调用 [**HS \_ 宿主 \_ 后 \_ 连接 \_ 身份验证 \_ 完成**](hs-host-post-connect-auth-completion.md) 处理程序，以通知主机请求的状态。

如果网络使用 EAP-SIM （也称为 "身份验证"），则该插件不应执行处于此状态的任何活动。 但是，如果网络需要基于 HTTP 的身份验证，则该插件必须执行相应的身份验证。

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


[**HS \_ 连接 \_ 上下文**](hs-connection-context.md)

[**HS \_ SIM \_ 数据**](hs-sim-data.md)

[**HS \_ 网络 \_ 标识**](hs-network-identity.md)

[**HS \_ 网络 \_ 配置文件**](hs-network-profile.md)

 

 




