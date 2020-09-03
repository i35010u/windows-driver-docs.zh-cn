---
title: HS_SIM_DATA 结构
description: HS_SIM_DATA 结构包含 SIM 卡中存储的信息。
ms.assetid: 9e29a85e-e764-4841-b218-c63bba0ca9fa
keywords:
- 从 Windows Vista 开始 HS_SIM_DATA 结构网络驱动程序
- 从 Windows Vista 开始 PHS_SIM_DATA 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5357a1605032fc988e296ebfba2ed072da627c35
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402978"
---
# <a name="hs_sim_data-structure"></a>HS \_ SIM \_ 数据结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ sim \_ 数据**结构包含 SIM 卡中存储的信息。

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
SIM 卡中存储 (ICCID) 的集成卡标识符。

**wszIMEI**  
国际移动设备标识 (IMEI) 用于标识3GPP 手机。

**wszMEID \_**  
由3GPP2 定义的移动设备标识符 (MEID) 。

**wszSF \_ EUIMID**  
为 R-UIM 或 CSIM (CDMA SIM 应用程序) 卡 (EUIMID) 扩展了短格式的用户标识模块标识符。

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
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




