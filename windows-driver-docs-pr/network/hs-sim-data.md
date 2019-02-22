---
title: HS_SIM_DATA 结构
description: HS_SIM_DATA 结构包含存储在 SIM 卡的信息。
ms.assetid: 9e29a85e-e764-4841-b218-c63bba0ca9fa
keywords:
- HS_SIM_DATA 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_SIM_DATA 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5472ef1830e08cbea36a9fa879b22adde3614bbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533014"
---
# <a name="hssimdata-structure"></a>HS\_SIM\_数据结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_SIM\_数据**结构包含存储在 SIM 卡的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_SIM_DATA {
  WCHAR wszICCID[HS_CONST_MAX_ICCID_LENGTH+1];
  WCHAR wszIMEI[HS_CONST_MAX_IMEI_LENGTH+1];
  WCHAR wszMEID_ME[HS_CONST_MAX_MEID_ME_LENGTH+1];
  WCHAR wszSF_EUIMID[HS_CONST_MAX_SF_EUIMID_LENGTH+1];
} HS_SIM_DATA, *PHS_SIM_DATA;
```

<a name="members"></a>成员
-------

**wszICCID**  
集成电路卡标识符 (ICCID) 存储在 SIM 卡中。

**wszIMEI**  
国际移动设备标识 (IMEI) 用于标识 3GPP 手机。

**wszMEID\_ME**  
移动设备标识符 (MEID) 由 3GPP2 定义。

**wszSF\_EUIMID**  
短格式扩展的用户标识模块标识符 (EUIMID) R UIM 或 CSIM （CDMA SIM 应用程序） 卡。

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

 

 




