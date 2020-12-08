---
title: HS_PLUGIN_QUERY_SUPPORTED_SIMS 函数
description: HS_PLUGIN_QUERY_SUPPORTED_SIMS 函数返回插件支持的 Sim 列表。
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_QUERY_SUPPORTED_SIMS 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc4208e16431f24f81fd24554082dff88e481078
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786173"
---
# <a name="hs_plugin_query_supported_sims-function"></a>HS \_ 插件 \_ 查询 \_ 支持的 \_ sim 函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 查询支持的 \_ \_ sim** 函数返回插件支持的 sim 列表。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_SUPPORTED_SIMS)(
  _In_opt_ HS_NETWORK_IDENTITY      *pNetworkIdentity,
  _Inout_  HS_PLUGIN_SUPPORTED_SIMS *pSupportedSIMs
);
```

<a name="parameters"></a>参数
----------

*\* pNetworkIdentity* \[ in，可选\]  
用于唯一标识网络的 [**HS \_ 网络 \_ 标识**](hs-network-identity.md) 结构。

*\* pSupportedSIMs* \[ ，out\]  
指向一个或多个 HS 插件的数组的指针 [**\_ 支持的 \_ \_ sim**](hs-plugin-supported-sims.md) 结构，其中包含支持的 sim 的列表。

<a name="return-value"></a>返回值
------------

宿主调用此函数以与插件通信，而不返回值。

<a name="remarks"></a>备注
-------

如果 *pNetworkIdentity* 参数存在，则必须提供连接到指定网络所需的 SIM 标识，否则必须提供用于连接到所有网络的全部 sim 列表。

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


[**HS \_ 网络 \_ 标识**](hs-network-identity.md)

[**HS \_ 插件 \_ 支持的 \_ SIM**](hs-plugin-supported-sims.md)

 

 




