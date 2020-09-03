---
title: HS_PLUGIN_STOP_POST_CONNECT_AUTH 函数
description: 调用 HS_PLUGIN_STOP_POST_CONNECT_AUTH 函数以通知插件停止身份验证过程。
ms.assetid: 2e4e01b1-e41a-41db-a3ca-6cc6b53b3a8b
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_STOP_POST_CONNECT_AUTH 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: a28b3fedee10cc79cbb0d01d925793e59e1eb9df
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402992"
---
# <a name="hs_plugin_stop_post_connect_auth-function"></a>HS \_ 插件 \_ 停止 \_ 后 \_ 连接 \_ 身份验证功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


将调用 **HS \_ 插件 " \_ 停止 \_ 后连接" \_ \_ 身份** 验证功能，通知插件停止身份验证过程。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_STOP_POST_CONNECT_AUTH)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>参数
----------

* \* pNetworkIdentity* \[\]  
用于唯一标识网络的 [**HS \_ 网络 \_ 标识**](hs-network-identity.md) 结构。

<a name="return-value"></a>返回值
------------

宿主调用此函数以与插件通信，而不返回值。

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


[**HS \_ 网络 \_ 标识**](hs-network-identity.md)

 

 




