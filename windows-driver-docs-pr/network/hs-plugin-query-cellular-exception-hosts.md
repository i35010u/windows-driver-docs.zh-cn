---
title: HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS 函数
description: HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS 函数在其身份验证过程中查询插件将需要通过手机网络连接到的主机列表。
ms.assetid: 7f38f146-a637-4ec3-8610-ea4934c4a57a
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d2702c640bb5b9d940c96483ba1a3ffaf0b311c
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403024"
---
# <a name="hs_plugin_query_cellular_exception_hosts-function"></a>HS \_ 插件 \_ 查询 \_ 手机网络 \_ 异常 \_ 主机功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 查询 \_ 手机网络 \_ 例外 \_ 主机**函数查询插件将需要通过手机网络连接到的主机列表作为其身份验证过程的一部分。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS)(
  _Inout_ HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS *pExceptionsList
);
```

<a name="parameters"></a>参数
----------

* \* pExceptionsList* \[ ，out\]  
[**HS \_ 插件 \_ 手机网络 \_ 异常 \_ 承载**](hs-plugin-cellular-exception-hosts.md)包含移动电话主机名称列表的结构。

<a name="return-value"></a>返回值
------------

宿主调用此函数以与插件通信，而不返回值。

<a name="remarks"></a>备注
-------

仅当插件将其[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)的 " **dwNumCellularExceptions** " 字段设置为大于零的值时，才会调用此函数。

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


[**HS \_ 插件 \_ 手机网络 \_ 例外 \_ 主机**](hs-plugin-cellular-exception-hosts.md)

[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)

 

 




