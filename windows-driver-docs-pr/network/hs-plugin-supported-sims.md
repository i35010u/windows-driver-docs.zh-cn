---
title: HS_PLUGIN_SUPPORTED_SIMS 结构
description: HS_PLUGIN_SUPPORTED_SIMS 结构包含支持的 SIM 配置的列表。 如果热点插件需要其网络的任何 HTTP 或 EAP 身份验证，必须提供此列表。
ms.assetid: 7ec8fb95-b227-4feb-882e-457a9ad6ec3e
keywords:
- HS_PLUGIN_SUPPORTED_SIMS 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_PLUGIN_SUPPORTED_SIMS 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43c7d45a0ded04a285cedbd793534a7078fa2436
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322135"
---
# <a name="hspluginsupportedsims-structure"></a>HS\_插件\_支持\_SIMS 结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_支持\_SIMS**结构包含支持的 SIM 配置的列表。 如果热点插件需要其网络的任何 HTTP 或 EAP 身份验证，必须提供此列表。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_SUPPORTED_SIMS {
  DWORD           dwCount;
  HS_SIM_IDENTITY pSupportedSIMs[*];
  HS_SIM_IDENTITY pSupportedSIMs[1];
} HS_PLUGIN_SUPPORTED_SIMS, *PHS_PLUGIN_SUPPORTED_SIMS;
```

<a name="members"></a>成员
-------

**dwCount**  
列表的大小。

**pSupportedSIMs**  
仅当使用 MIDL 使用。 唯一的大小为 (dwCount)。

一个数组 HS\_SIM\_标识结构组成的列表的受支持的 SIM 配置。

**pSupportedSIMs**  
使用 MIDL 未被使用。

一个数组 HS\_SIM\_标识结构组成的列表的受支持的 SIM 配置。

<a name="remarks"></a>备注
-------

在中**dwEapMethods**字段[ **HS\_SIM\_标识**](hs-sim-identity.md)结构对于每个 SIM 配置，您必须指定 EAP 方法，它支持。

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


[**HS\_SIM\_标识**](hs-sim-identity.md)

[Microsoft 接口定义语言](https://msdn.microsoft.com//library/windows/desktop/aa367091)

 

 




