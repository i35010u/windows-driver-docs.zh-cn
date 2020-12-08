---
title: HS_NETWORK_PROFILE 结构
description: HS_NETWORK_PROFILE 结构由插件提供，并包含连接到目标网络所需的信息。 网络配置文件的每个实例都与相应的 HS_NETWORK_IDENTITY 结构唯一关联。
keywords:
- 从 Windows Vista 开始 HS_NETWORK_PROFILE 结构网络驱动程序
- 从 Windows Vista 开始 PHS_NETWORK_PROFILE 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f15bf178eb6327f3723a1870e2ab253ccd716d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814155"
---
# <a name="hs_network_profile-structure"></a>HS \_ 网络 \_ 配置文件结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 网络 \_ 配置文件** 结构由插件提供，并包含连接到目标网络所需的信息。 网络配置文件的每个实例都与相应的 [**HS \_ 网络 \_ 标识**](hs-network-identity.md) 结构唯一关联。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_NETWORK_PROFILE {
  DWORD  dwNetworkCapabilities;
  USHORT usPriority;
  DWORD  dwSupportedSIMCount;
  DWORD  dmNumCellularExceptions;
  DWORD  dwNetworkStringID;
  DWORD  dwKeepAliveTimeMins;
  WCHAR  szRealm[HS_CONST_MAX_REALM_LENGTH+1];
} HS_NETWORK_PROFILE, *PHS_NETWORK_PROFILE;
```

<a name="members"></a>成员
-------

**dwNetworkCapabilities**  
可能的 **HS \_ 标志 \_ 功能 \_ 网络 \_ \\** _ 值的子集。 有关热点主机功能的详细信息，请参阅 [_ *Wi-fi 热点卸载常数* *](wi-fi-hotspot-offloading-constants.md)。

**usPriority**  
分配给关联网络的唯一优先级值。 该值必须是介于1和65000之间的值 (隐藏网络的值必须为 1) 。 数值越小，优先级越高。

**dwSupportedSIMCount**  
支持的 SIM 计数。 此成员设置为基于 HTTP 和 EAP-SIM/也称 "身份验证"。

**dmNumCellularExceptions**  
可选。 仅通过蜂窝的主机连接数。

**dwNetworkStringID**  
网络名称字符串 ID。 最大字符串大小 = 最大 \_ 网络 \_ 显示 \_ 名称 \_ 长度。

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
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**HS \_ 网络 \_ 标识**](hs-network-identity.md)

[**Wi-Fi 热点卸载常量**](wi-fi-hotspot-offloading-constants.md)

 

 




