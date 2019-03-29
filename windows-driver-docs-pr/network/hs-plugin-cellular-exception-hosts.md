---
title: HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 结构
description: HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 结构包含该插件要求仅在身份验证过程，通过移动电话的持有者要连接的主机的列表。
ms.assetid: cc7ad05b-d03b-463a-9d22-1982aee882e8
keywords:
- HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ad326027b0224e567930c3f409f16c8e219951a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565291"
---
# <a name="hsplugincellularexceptionhosts-structure"></a>HS\_插件\_移动电话\_异常\_主机结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_移动电话\_异常\_主机**结构包含的主机插件所需的用于通过移动电话持有者仅在连接列表身份验证过程。 这是可以请求通过该插件的可选功能。 有关详细信息，请参阅[ **HS\_插件\_查询\_移动电话\_异常\_主机**](hs-plugin-query-cellular-exception-hosts.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS {
  DWORD               dwCount;
  HS_PLUGIN_HOST_NAME pExceptions[*];
  HS_PLUGIN_HOST_NAME pExceptions[1];
} HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS, *PHS_PLUGIN_CELLULAR_EXCEPTION_HOSTS;
```

<a name="members"></a>成员
-------

**dwCount**  
指向主机名列表中的数字**pExceptions**。

**pExceptions**  
仅当使用 MIDL 使用。 唯一的大小为 (dwCount)。

指向主机名的列表的指针。

**pExceptions**  
使用 MIDL 未被使用。

指向主机名的列表的指针。

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


[**HS\_插件\_查询\_移动电话\_异常\_主机**](hs-plugin-query-cellular-exception-hosts.md)

[Microsoft 接口定义语言](https://msdn.microsoft.com//library/windows/desktop/aa367091)

 

 




