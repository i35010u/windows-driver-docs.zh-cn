---
title: HS_PLUGIN_SUPPORTED_SIMS 结构
description: HS_PLUGIN_SUPPORTED_SIMS 结构包含受支持的 SIM 配置的列表。 如果热点插件要求对其任何网络进行 HTTP 或 EAP 身份验证，则必须提供此列表。
ms.assetid: 7ec8fb95-b227-4feb-882e-457a9ad6ec3e
keywords:
- 从 Windows Vista 开始 HS_PLUGIN_SUPPORTED_SIMS 结构网络驱动程序
- 从 Windows Vista 开始 PHS_PLUGIN_SUPPORTED_SIMS 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ed0faea390237324d4aa8e4c8b1f02a920f67f3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216194"
---
# <a name="hs_plugin_supported_sims-structure"></a>HS \_ 插件 \_ 支持的 \_ sim 结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件支持 \_ 的 \_ sim**结构包含受支持的 SIM 配置的列表。 如果热点插件要求对其任何网络进行 HTTP 或 EAP 身份验证，则必须提供此列表。

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
列表大小。

**pSupportedSIMs**  
如果使用了 MIDL，则使用。 唯一，大小是 (dwCount) 。

一个由 HS \_ sim 标识结构组成的数组 \_ ，其中列出了受支持的 sim 配置的列表。

**pSupportedSIMs**  
如果未使用 MIDL，则使用。

一个由 HS \_ sim 标识结构组成的数组 \_ ，其中列出了受支持的 sim 配置的列表。

<a name="remarks"></a>备注
-------

在每个 SIM 配置的[**HS \_ SIM \_ 标识**](hs-sim-identity.md)结构的**dwEapMethods**字段中，你必须指定它支持的 EAP 方法。

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

## <a name="see-also"></a>另请参阅


[**HS \_ SIM \_ 标识**](hs-sim-identity.md)

[Microsoft 接口定义语言](/windows/desktop/Midl/midl-start-page)

 

