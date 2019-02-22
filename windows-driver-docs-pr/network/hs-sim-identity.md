---
title: HS_SIM_IDENTITY 结构
description: HS_SIM_IDENTITY 结构包含 SIM EAP-SIM 或 EAP-AKA 身份验证所需的标识信息。
ms.assetid: b45fac33-79de-4006-9dcb-95725be11ec1
keywords:
- HS_SIM_IDENTITY 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_SIM_IDENTITY 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f1e8b3931fd6dd90e84f413d0e531ad02d9035c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554477"
---
# <a name="hssimidentity-structure"></a>HS\_SIM\_IDENTITY 结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_SIM\_标识**结构包含 SIM EAP-SIM 或 EAP-AKA 身份验证所需的标识信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_SIM_IDENTITY {
  eHS_SIM_TYPE SimType;
  DWORD        dwMNC;
  DWORD        dwMCC;
  DWORD        dwNID;
  DWORD        dwSID;
  DWORD        dwEapMethods;
} HS_SIM_IDENTITY, *PHS_SIM_IDENTITY;
```

<a name="members"></a>成员
-------

**SimType**  
Sim 卡的类型、 是否 GSM 或 CDMA，或 none。 如果网络 GSM， **dwMNC**和**dwMCC**将定义两个字段，而对于 CDMA **dwSID**并**dwNID**两个字段必须定义。

**dwMNC**  
如果 SIM GSM 类型，使用。

GSM 网络移动电话网络代码 （mnc)。

**dwMCC**  
如果 SIM GSM 类型，使用。

GSM 网络移动的国家/地区代码 (MCC)。

**dwNID**  
如果 SIM CDMA 类型，使用。

网络标识数 (NID) 的 CDMA 网络。

**dwSID**  
如果 SIM CDMA 类型，使用。

系统标识号 (SID) 的 CDMA 网络。

**dwEapMethods**  
EAP 身份验证方法。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[可扩展的身份验证协议](https://msdn.microsoft.com/library/windows/desktop/aa363502)

 

 




