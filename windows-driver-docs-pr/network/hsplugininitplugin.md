---
title: HSPluginInitPlugin 函数
description: HSPluginInitPlugin 函数导出由插件 DLL，并调用以初始化该插件。
ms.assetid: db51267c-4f38-47bd-bde2-7b27a93dd2a7
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 HSPluginInitPlugin 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: eed897d595c0fa549e51dd86e6a445bcdcb02294
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566656"
---
# <a name="hsplugininitplugin-function"></a>HSPluginInitPlugin 函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HSPluginInitPlugin**由插件 DLL 导出函数，并调用以初始化该插件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DWORD HSPluginInitPlugin(
  _In_  HANDLE                hPluginContext,
  _In_  DWORD                 dwVerNumUsed,
  _In_  DWORD                 dwHostCapabilities,
  _In_  HS_DEVICE_IDENTITY    *pDeviceIdentity,
  _In_  HOTSPOT_HOST_HANDLERS *pHotspotHostHandlers,
  _Out_ HOTSPOT_PLUGIN_APIS   *pHotspotPluginAPIs,
  _Out_ HS_PLUGIN_PROFILE     *pPluginProfile
);
```

<a name="parameters"></a>Parameters
----------

*hPluginContext* \[in\]  
宿主提供了句柄，该插件，则需要保存，然后使用需要向通过主机的主机的处理程序函数发出请求时。

*dwVerNumUsed* \[in\]  
主机的当前版本号。

*dwHostCapabilities* \[in\]  
指定的主机可以向该插件提供的功能的列表的值。 此值是适用的功能标志的按位 OR 组合。 有关功能标志的详细信息，请参阅**HS\_标志\_功能\_\\*** 中的常量[**的 Wi-fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md).

**请注意**  如果主机未提供所需的插件的所有功能，将不会初始化该插件。

 

*\*pDeviceIdentity* \[in\]  
指向[ **HS\_设备\_标识**](hs-device-identity.md)结构，其中包含有关设备制造商和型号的信息。

*\*pHotspotHostHandlers* \[in\]  
指向[**热点\_主机\_处理程序**](hotspot-host-handlers.md)结构，其中包含热点主机处理程序函数表。 此表包含指向与热点主机通信的插件由调用的函数的指针。

*\*pHotspotPluginAPIs* \[out\]  
指向[**热点\_插件\_API** ](hotspot-plugin-apis.md)结构，其中包含热点插件 Api 函数表。 此表返回的插件，并包含指向由主机进行通信使用插件调用的函数的指针。

*\*pPluginProfile* \[out\]  
指向[ **HS\_插件\_配置文件**](hs-plugin-profile.md)结构，返回的插件，提供有关插件的信息。

<a name="remarks"></a>备注
-------

在初始化期间，主机提供以下功能：

-   插件上下文句柄
-   当前的版本号
-   主机可以向该插件提供的功能的列表
-   通过该插件可以与主机通信的主机处理程序函数表指向的指针

该插件将指针返回到其自身函数表和一个指向其[ **HS\_插件\_配置文件**](hs-plugin-profile.md)结构。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**Wi-fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md)

[**HS\_设备\_标识**](hs-device-identity.md)

[**热点\_主机\_处理程序**](hotspot-host-handlers.md)

[**热点\_插件\_API**](hotspot-plugin-apis.md)

[**HS\_插件\_配置文件**](hs-plugin-profile.md)

 

 




