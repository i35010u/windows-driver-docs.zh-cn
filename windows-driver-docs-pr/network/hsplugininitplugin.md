---
title: HSPluginInitPlugin 函数
description: HSPluginInitPlugin 函数由插件 DLL 导出，并调用来初始化插件。
keywords:
- 从 Windows Vista 开始的 HSPluginInitPlugin 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae6735e778275e2d057e22799dd63df32b986519
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839483"
---
# <a name="hsplugininitplugin-function"></a>HSPluginInitPlugin 函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HSPluginInitPlugin** 函数由插件 DLL 导出，并调用来初始化插件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DWORD HSPluginInitPlugin(
  _In_  HANDLE                hPluginContext,
  _In_  DWORD                 dwVerNumUsed,
  _In_  DWORD                 dwHostCapabilities,
  _In_  HS_DEVICE_IDENTITY    *pDeviceIdentity,
  _In_  HOTSPOT_HOST_HANDLERS *pHotspotHostHandlers,
  _Out_ HOTSPOT_PLUGIN_APIS   *pHotspotPluginAPIs,
  _Out_ HS_PLUGIN_PROFILE     *pPluginProfile
);
```

<a name="parameters"></a>参数
----------

*hPluginContext* \[中\]  
宿主提供的一个句柄，它要求插件保存，然后在需要通过宿主处理程序函数向宿主发出请求时使用。

*dwVerNumUsed* \[中\]  
宿主的当前版本号。

*dwHostCapabilities* \[中\]  
值，指定主机可提供给插件的功能列表。 此值是适用功能标志的按位 "或" 组合。 有关功能标志的详细信息，请参阅中的 **HS \_ 标志 \_ 功能 \_ \\** _ [常量 *-wi-fi 热点卸载常数* *](wi-fi-hotspot-offloading-constants.md)。

**注意**  如果主机未提供插件所需的所有功能，则不会初始化插件。

 

*\* pDeviceIdentity* \[\]  
一个指针，指向包含有关设备制造商和型号的信息的 [**HS \_ 设备 \_ 标识**](hs-device-identity.md) 结构。

*\* pHotspotHostHandlers* \[\]  
指向 [**热点 \_ 主机 \_ 处理程序**](hotspot-host-handlers.md) 结构的指针，该结构包含热点主机处理程序函数表。 此表包含指向插件调用的函数的指针，这些函数用于与热点主机通信。

*\* pHotspotPluginAPIs* \[\]  
指向 [**热点 \_ 插件 \_ api**](hotspot-plugin-apis.md) 结构的指针，该结构包含热点插件 api 函数表。 此表由插件返回，并包含指向函数调用的函数的指针，这些函数用于与插件通信。

*\* pPluginProfile* \[\]  
指向由插件返回的 [**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md) 结构的指针，该结构提供有关插件的信息。

<a name="remarks"></a>备注
-------

在初始化期间，主机提供以下内容：

-   插件上下文句柄
-   当前版本号
-   主机可提供给插件的功能列表
-   指向主机处理函数表的指针，该函数通过该函数可以与主机进行通信

此插件返回一个指向其自己的函数表的指针，以及一个指向其 [**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md) 结构的指针。

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
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**Wi-Fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md)

[**HS \_ 设备 \_ 标识**](hs-device-identity.md)

[**热点 \_ 主机 \_ 处理程序**](hotspot-host-handlers.md)

[**热点 \_ 插件 \_ API**](hotspot-plugin-apis.md)

[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)

 

 




