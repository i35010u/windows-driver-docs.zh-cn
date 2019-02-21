---
title: HS_PLUGIN_QUERY_SUPPORTED_SIMS 函数
description: HS_PLUGIN_QUERY_SUPPORTED_SIMS 函数返回的插件支持的 Sim 的列表。
ms.assetid: e1b41bb1-7f82-4298-b070-20cb557fa0fc
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_QUERY_SUPPORTED_SIMS) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20c7948c6769893e6147fc5b774d1e61f8282214
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525167"
---
# <a name="hspluginquerysupportedsims-function"></a>HS\_插件\_查询\_支持\_SIMS 函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_查询\_支持\_SIMS**函数返回的插件支持的 Sim 的列表。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_SUPPORTED_SIMS)(
  _In_opt_ HS_NETWORK_IDENTITY      *pNetworkIdentity,
  _Inout_  HS_PLUGIN_SUPPORTED_SIMS *pSupportedSIMs
);
```

<a name="parameters"></a>参数
----------

*\*pNetworkIdentity* \[in, optional\]  
[ **HS\_网络\_标识**](hs-network-identity.md)唯一标识网络的结构。

*\*pSupportedSIMs* \[in、 out\]  
指向数组的一个或多个指针[ **HS\_插件\_支持\_SIMS** ](hs-plugin-supported-sims.md)列出的受支持的 Sim 的结构。

<a name="return-value"></a>返回值
------------

此函数调用由宿主与插件进行通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

如果*pNetworkIdentity*参数存在，则必须提供连接到指定的网络所需这些 SIM 标识，否则必须提供用于连接到所有网络 Sim 的完整列表。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**HS\_NETWORK\_IDENTITY**](hs-network-identity.md)

[**HS\_插件\_支持\_SIMS**](hs-plugin-supported-sims.md)

 

 




