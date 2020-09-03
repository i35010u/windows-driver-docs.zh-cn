---
title: HS_PLUGIN_QUERY_HIDDEN_NETWORK 函数
description: HS_PLUGIN_QUERY_HIDDEN_NETWORK 函数返回隐藏网络的网络标识和网络配置文件。
ms.assetid: edf5ddb0-22f6-4c24-a118-3915a1f2b0af
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_QUERY_HIDDEN_NETWORK 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3998544e68bbae5311778b9f53a1e42240a02f28
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403022"
---
# <a name="hs_plugin_query_hidden_network-function"></a>HS \_ 插件 \_ 查询 \_ 隐藏 \_ 网络函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 查询 \_ 隐藏 \_ 网络**函数返回隐藏网络的网络标识和网络配置文件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_HIDDEN_NETWORK)(
  _Out_ HS_NETWORK_IDENTITY *pHiddenNetworkIdentity,
  _Out_ HS_NETWORK_PROFILE  *pHiddenNetworkProfile
);
```

<a name="parameters"></a>参数
----------

* \* pHiddenNetworkIdentity* \[\]  
用于唯一标识网络的 [**HS \_ 网络 \_ 标识**](hs-network-identity.md) 结构。

* \* pHiddenNetworkProfile* \[\]  
包含网络配置文件的 [**HS \_ 网络 \_ 配置文件**](hs-network-profile.md) 结构。

<a name="return-value"></a>返回值
------------

宿主调用此函数以与插件通信，而不返回值。

<a name="remarks"></a>备注
-------

仅当关联插件的[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)结构的**dwPluginCapabilities**字段包含**HS \_ 标志 \_ 功能 \_ 网络 \_ 类型 \_ 隐藏**功能时，主机才调用此函数。

插件必须为隐藏的 Wi-fi 网络提供网络标识和网络配置文件。

此网络必须在所有热点网络中具有最高优先级 (1) 。

热点卸载服务在服务的生命周期内对一个隐藏的网络施加限制。 因此，在安装了多个插件的情况下，只接受第一个插件指定隐藏网络的请求。

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


[**HS \_ 网络 \_ 标识**](hs-network-identity.md)

[**HS \_ 网络 \_ 配置文件**](hs-network-profile.md)

[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)

 

 




