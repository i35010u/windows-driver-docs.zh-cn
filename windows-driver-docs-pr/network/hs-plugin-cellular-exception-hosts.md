---
title: HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 结构
description: HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 结构包含在身份验证过程中，插件只需通过蜂窝持有者连接的主机列表。
keywords:
- 从 Windows Vista 开始 HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 结构网络驱动程序
- 从 Windows Vista 开始 PHS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: d496981de33418956ad21bbfe6acc78c19b5e9b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814143"
---
# <a name="hs_plugin_cellular_exception_hosts-structure"></a>HS \_ 插件 \_ 手机网络 \_ 异常 \_ 托管结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 手机网络 \_ 例外 \_ 主机** 结构包含在身份验证过程中，该插件只需通过蜂窝持有者连接的主机列表。 这是可由插件请求的可选功能。 有关详细信息，请参阅 [**HS \_ 插件 \_ 查询 \_ 手机网络 \_ 异常 \_ 主机**](hs-plugin-query-cellular-exception-hosts.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS {
  DWORD               dwCount;
  HS_PLUGIN_HOST_NAME pExceptions[*];
  HS_PLUGIN_HOST_NAME pExceptions[1];
} HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS, *PHS_PLUGIN_CELLULAR_EXCEPTION_HOSTS;
```

<a name="members"></a>成员
-------

**dwCount**  
**PExceptions** 所指向的列表中的主机名数。

**pExceptions**  
如果使用了 MIDL，则使用。 唯一，大小是 (dwCount) 。

指向主机名列表的指针。

**pExceptions**  
如果未使用 MIDL，则使用。

指向主机名列表的指针。

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


[**HS \_ 插件 \_ 查询 \_ 手机网络 \_ 异常 \_ 主机**](hs-plugin-query-cellular-exception-hosts.md)

[Microsoft 接口定义语言](/windows/desktop/Midl/midl-start-page)

 

