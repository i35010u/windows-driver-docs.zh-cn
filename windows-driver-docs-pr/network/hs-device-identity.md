---
title: HS_DEVICE_IDENTITY 结构
description: HS_DEVICE_IDENTITY 结构包含的设备型号和制造商信息。
ms.assetid: 4a679fb2-d5b1-4635-9422-a21a316b360c
keywords:
- HS_DEVICE_IDENTITY 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_DEVICE_IDENTITY 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe8a59888b032657a764bca0b7dfcfc0d763e79f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349693"
---
# <a name="hsdeviceidentity-structure"></a>HS\_设备\_IDENTITY 结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_设备\_标识**结构包含的设备型号和制造商信息。

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
Sim 卡的类型、 是否 GSM 或 CDMA。

**wszPhoneManufacturer**  
电话制造商名称。

**wszPhoneModelName**  
电话模型名称。

**wszPhoneManufacturerModel**  
电话制造商和型号的另一个名称。

**wszDeviceModel**  
设备模型名称。

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

 

 




