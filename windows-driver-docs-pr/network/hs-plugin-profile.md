---
title: HS_PLUGIN_PROFILE 结构
description: HS_PLUGIN_PROFILE 结构提供有关插件的信息。 此结构的成员由插件在执行由主机调用的 HSPluginInitPlugin 函数期间进行设置。
ms.assetid: 0c4f7088-737e-479a-b46e-a55e96719775
keywords:
- 从 Windows Vista 开始 HS_PLUGIN_PROFILE 结构网络驱动程序
- 从 Windows Vista 开始 PHS_PLUGIN_PROFILE 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8e913ef165accaeaac3fd9658e1f66d4abf76de
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403026"
---
# <a name="hs_plugin_profile-structure"></a>HS \_ 插件 \_ 配置文件结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 配置文件**结构提供有关插件的信息。 此结构的成员由插件在执行由主机调用的 [**HSPluginInitPlugin**](hsplugininitplugin.md) 函数期间进行设置。

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

可能的**HS \_ 标志 \_ 功能 \_ NETWORK \_ \\ *** 值的子集。 有关热点主机功能的详细信息，请参阅 [**Wi-fi 热点卸载常数**](wi-fi-hotspot-offloading-constants.md)。

**dwNumNetworksSupported**  
必需。

此插件支持的网络总数。

**dwProviderNameStringID**  
必需。

向用户显示的网络提供程序名称。 最大字符串大小 = 最大 \_ 提供程序 \_ 名称 \_ 长度。

**dwGenericNetworkNameStringID**  
可选。

网络名称。 最大字符串大小 = 最大 \_ 网络 \_ 显示 \_ 名称 \_ 长度。

**dwAdvancedPageStringID**  
可选。

最大字符串大小 = 最大长度为 HS \_ \_ 的常量最大值 \_ \_ \_ \_ 。

**dwProfileUpdateTimeDays**  
可选。

必须大于或等于最小为 HS \_ 常量 \_ \_ 的配置文件 \_ 更新时间（天） \_ \_ \_ 。

**szRealm**  
如果 \_ 设置了 "HS 标志 \_ 功能" \_ 网络 \_ 自定义 \_ 领域，则是必需的。

特定于网络的领域值。

**dwSupportedSIMCount**  
**PSupported sim**指向的列表的大小。

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
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**HSPluginInitPlugin**](hsplugininitplugin.md)

[**Wi-Fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md)

 

 




