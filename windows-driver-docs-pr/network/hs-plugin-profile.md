---
title: HS_PLUGIN_PROFILE 结构
description: HS_PLUGIN_PROFILE 结构提供了有关该插件的信息。 由主机调用 HSPluginInitPlugin 函数执行期间，该插件会设置此结构的成员。
ms.assetid: 0c4f7088-737e-479a-b46e-a55e96719775
keywords:
- HS_PLUGIN_PROFILE 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_PLUGIN_PROFILE 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b5e46347b4008af7c7e14926e9ffa32a9ae982
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322189"
---
# <a name="hspluginprofile-structure"></a>HS\_插件\_配置文件结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_配置文件**结构提供了有关该插件的信息。 此结构的成员由插件设置的执行过程[ **HSPluginInitPlugin** ](hsplugininitplugin.md)由主机调用的函数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_PROFILE {
  DWORD dwPluginCapabilities;
  DWORD dwNumNetworksSupported;
  DWORD dwProviderNameStringID;
  DWORD dwGenericNetworkNameStringID;
  DWORD dwAdvancedPageStringID;
  DWORD dwProfileUpdateTimeDays;
  WCHAR szRealm[HS_CONST_MAX_REALM_LENGTH+1];
  DWORD dwSupportedSIMCount;
} HS_PLUGIN_PROFILE, *PHS_PLUGIN_PROFILE;
```

<a name="members"></a>成员
-------

**dwPluginCapabilities**  
必需。

可能的一个子集**HS\_标志\_功能\_网络\_\\*** 值。 热点主机功能的详细信息，请参阅[ **Wi-fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md)。

**dwNumNetworksSupported**  
必需。

此插件支持的网络的总数。

**dwProviderNameStringID**  
必需。

向用户显示网络提供程序名称。 最大字符串大小 = MAX\_提供程序\_名称\_长度。

**dwGenericNetworkNameStringID**  
可选。

网络名称。 最大字符串大小 = MAX\_网络\_显示\_名称\_长度。

**dwAdvancedPageStringID**  
可选。

最大字符串大小 = HS\_常量\_最大\_高级\_页\_字符串\_长度。

**dwProfileUpdateTimeDays**  
可选。

必须是大于或等于 HS\_常量\_MIN\_配置文件\_更新\_时间\_IN\_天。

**szRealm**  
如果使用 HS\_标志\_功能\_网络\_自定义\_领域设置。

特定于网络的领域值。

**dwSupportedSIMCount**  
指向列表的大小**pSupported SIMs**。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**HSPluginInitPlugin**](hsplugininitplugin.md)

[**Wi-fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md)

 

 




