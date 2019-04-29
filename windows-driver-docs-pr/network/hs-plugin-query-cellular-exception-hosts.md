---
title: HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS 函数
description: HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS 函数查询该插件需要作为其身份验证过程的一部分通过移动电话网络连接到的主机的列表。
ms.assetid: 7f38f146-a637-4ec3-8610-ea4934c4a57a
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d0658d58919e081417e17c00603ac29a7d962dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322169"
---
# <a name="hspluginquerycellularexceptionhosts-function"></a>HS\_插件\_查询\_移动电话\_异常\_主机函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_查询\_手机\_异常\_主机**函数查询该插件需要作为的一部分通过移动电话网络连接到的主机的列表其身份验证过程。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS)(
  _Inout_ HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS *pExceptionsList
);
```

<a name="parameters"></a>Parameters
----------

*\*pExceptionsList* \[in、 out\]  
[ **HS\_插件\_手机\_异常\_主机**](hs-plugin-cellular-exception-hosts.md)结构，其中包含移动电话网络的主机名的列表。

<a name="return-value"></a>返回值
------------

此函数调用由宿主与插件进行通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

仅当该插件设置调用此函数**dwNumCellularExceptions**的字段及其[ **HS\_插件\_配置文件**](hs-plugin-profile.md)为值大于零。

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


[**HS\_PLUGIN\_CELLULAR\_EXCEPTION\_HOSTS**](hs-plugin-cellular-exception-hosts.md)

[**HS\_插件\_配置文件**](hs-plugin-profile.md)

 

 




