---
title: HS_NETWORK_PROFILE 结构
description: HS_NETWORK_PROFILE 结构提供的插件，并包含连接到的目标网络所需的信息。 网络配置文件的每个实例都与相应的 HS_NETWORK_IDENTITY 结构唯一关联。
ms.assetid: 55e8786c-d7b8-48f3-9e54-312183cf8fb3
keywords:
- HS_NETWORK_PROFILE 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_NETWORK_PROFILE 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef670ed92132114119174230fc78532fe5ca6e44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568046"
---
# <a name="hsnetworkprofile-structure"></a>HS\_网络\_配置文件结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_网络\_配置文件**结构提供的插件和包含连接到的目标网络所需的信息。 网络配置文件的每个实例都与相应唯一关联[ **HS\_网络\_标识**](hs-network-identity.md)结构。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_NETWORK_PROFILE {
  DWORD  dwNetworkCapabilities;
  USHORT usPriority;
  DWORD  dwSupportedSIMCount;
  DWORD  dmNumCellularExceptions;
  DWORD  dwNetworkStringID;
  DWORD  dwKeepAliveTimeMins;
  WCHAR  szRealm[HS_CONST_MAX_REALM_LENGTH+1];
} HS_NETWORK_PROFILE, *PHS_NETWORK_PROFILE;
```

<a name="members"></a>成员
-------

**dwNetworkCapabilities**  
可能的一个子集**HS\_标志\_功能\_网络\_\\*** 值。 热点主机功能的详细信息，请参阅[ **Wi-fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md)。

**usPriority**  
分配给关联的网络的唯一的优先级值。 它必须是介于 1 和 65000 （隐藏的网络必须具有值为 1） 之间的值。 较低的数字值对应于更高的优先级。

**dwSupportedSIMCount**  
受支持的 SIM 计数。 此成员设置为基于 HTTP 和 SIM/AKA/EAP-AKA ' 身份验证。

**dmNumCellularExceptions**  
可选。 通过仅移动电话网络的主机连接数。

**dwNetworkStringID**  
网络名称的字符串 id。 最大字符串大小 = MAX\_网络\_显示\_名称\_长度。

**dwKeepAliveTimeMins**  
可选。 网络连接保持活动消息之间的时间间隔。

**szRealm**  
特定于网络的领域值。

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


[**HS\_NETWORK\_IDENTITY**](hs-network-identity.md)

[**Wi-fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md)

 

 




