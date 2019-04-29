---
title: HS_PLUGIN_QUERY_HIDDEN_NETWORK 函数
description: HS_PLUGIN_QUERY_HIDDEN_NETWORK 函数返回的网络标识和隐藏网络的网络配置文件。
ms.assetid: edf5ddb0-22f6-4c24-a118-3915a1f2b0af
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_QUERY_HIDDEN_NETWORK) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bcfcfef1f2fd519a2123bb8654a616744729563
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322173"
---
# <a name="hspluginqueryhiddennetwork-function"></a>HS\_插件\_查询\_HIDDEN\_网络函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_查询\_HIDDEN\_网络**函数返回的网络标识和隐藏网络的网络配置文件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_HIDDEN_NETWORK)(
  _Out_ HS_NETWORK_IDENTITY *pHiddenNetworkIdentity,
  _Out_ HS_NETWORK_PROFILE  *pHiddenNetworkProfile
);
```

<a name="parameters"></a>Parameters
----------

*\*pHiddenNetworkIdentity* \[out\]  
[ **HS\_网络\_标识**](hs-network-identity.md)唯一标识网络的结构。

*\*pHiddenNetworkProfile* \[out\]  
[ **HS\_网络\_配置文件**](hs-network-profile.md)结构，其中包含的网络配置文件。

<a name="return-value"></a>返回值
------------

此函数调用由宿主与插件进行通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

主机调用此函数仅当**dwPluginCapabilities**字段的关联插件[ **HS\_插件\_配置文件**](hs-plugin-profile.md)结构包括**HS\_标志\_功能\_网络\_类型\_HIDDEN**功能。

该插件必须为隐藏的 Wi-fi 网络提供的网络标识和网络配置文件。

此网络必须具有在所有热点网络之间的最高优先级 (1)。

热点卸载服务施加服务的生命周期的一个隐藏网络的限制。 因此，在这种情况其中有多个插件安装，仅第一个插件来指定隐藏的网络将从中接受请求。

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

[**HS\_NETWORK\_PROFILE**](hs-network-profile.md)

[**HS\_插件\_配置文件**](hs-plugin-profile.md)

 

 




