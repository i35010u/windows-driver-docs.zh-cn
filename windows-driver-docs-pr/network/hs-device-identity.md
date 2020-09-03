---
title: HS_DEVICE_IDENTITY 结构
description: HS_DEVICE_IDENTITY 结构包含有关设备型号和制造商的信息。
ms.assetid: 4a679fb2-d5b1-4635-9422-a21a316b360c
keywords:
- 从 Windows Vista 开始 HS_DEVICE_IDENTITY 结构网络驱动程序
- 从 Windows Vista 开始 PHS_DEVICE_IDENTITY 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 950f753859a1b48d165a6118741260d2dcb9c2f8
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403108"
---
# <a name="hs_device_identity-structure"></a>HS \_ 设备 \_ 标识结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 设备 \_ 标识**结构包含有关设备型号和制造商的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_DEVICE_IDENTITY {
  DWORD dwSystemType;
  WCHAR wszPhoneManufacturer[HS_CONST_MAX_DEVICE_INFO_LENGTH+1];
  WCHAR wszPhoneModelName[HS_CONST_MAX_DEVICE_INFO_LENGTH+1];
  WCHAR wszPhoneManufacturerModel[HS_CONST_MAX_DEVICE_INFO_LENGTH+1];
  WCHAR wszDeviceModel[HS_CONST_MAX_DEVICE_INFO_LENGTH+1];
} HS_DEVICE_IDENTITY, *PHS_DEVICE_IDENTITY;
```

<a name="members"></a>成员
-------

**dwSystemType**  
SIM 的类型，无论是 GSM 还是 CDMA。

**wszPhoneManufacturer**  
电话制造商名称。

**wszPhoneModelName**  
电话型号名称。

**wszPhoneManufacturerModel**  
电话制造商和型号的其他名称。

**wszDeviceModel**  
设备型号名称。

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

 

 




