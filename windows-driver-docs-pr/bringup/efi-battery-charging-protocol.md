---
title: EFI_BATTERY_CHARGING_PROTOCOL
description: EFI_BATTERY_CHARGING_PROTOCOL
ms.assetid: 978d063e-f864-44be-9f58-4e4c6b2193b8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff284993c68a58ac7635225fbdb32148f5ab7758
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532972"
---
# <a name="efibatterychargingprotocol"></a>EFI\_电池\_正在充电\_协议


此协议允许 UEFI 驱动程序支持的主电池充电。

## <a name="syntax"></a>语法


```cpp
// {840CB643-8198-428a-A8B3-A072CE57CDB9}
#define EFI_BATTERY_CHARGING_PROTOCOL_GUID \
  {0x840cb643, 0x8198, 0x428a, 0xa8, 0xb3, 0xa0, 0x72, 0xce, 0x57, 0xcd, 0xb9};

typedef struct _EFI_BATTERY_CHARGING_PROTOCOL {
  EFI_BATTERY_CHARGING_GET_BATTERY_STATUS         GetBatteryStatus;
  EFI_BATTERY_CHARGING_CHARGE_BATTERY             ChargeBattery; 
  UINT32                                          Revision;
  EFI_BATTERY_CHARGING_GET_BATTERY_INFORMATION    GetBatteryInformation;
} EFI_BATTERY_CHARGING_PROTOCOL;
```

## <a name="members"></a>成员


<a href="" id="getbatterystatus"></a>**GetBatteryStatus**  
返回有关主电池的当前状态的信息。

<a href="" id="chargebattery"></a>**ChargeBattery**  
为指定的级别使用指定的最大当前为主电池充电。

<a href="" id="revision"></a>**修订版本**  
修订了 EFI\_电池\_正在充电\_协议遵循。 所有未来的版本必须是向后兼容。 如果将来的版本不是向后兼容，必须使用不同的 GUID。

当前的修订版本是 0x00010002，但也支持修订 0x00010001。 有关哪些函数中每个版本的协议支持的详细信息，请参阅下面的备注部分。

<a href="" id="getbatteryinformation"></a>**GetBatteryInformation**  
返回有关主电池的当前状态的信息。 此函数是类似于**GetBatteryStatus**，但它提供的信息多于**GetBatteryStatus**。

## <a name="remarks"></a>备注


下表列出了 EFI 的每个版本中支持的函数\_电池\_正在充电\_协议协议。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>修订 0x00010002</th>
<th>修订 0x00010001</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>GetBatteryInformation</strong></p>
<p><strong>GetBatteryStatus</strong></p>
<p><strong>ChargeBattery</strong></p></td>
<td><p><strong>GetBatteryStatus</strong></p>
<p><strong>ChargeBattery</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题

[UEFI 电池充电协议](uefi-battery-charging-protocol.md)  

[EFI\_BATTERY\_CHARGING\_PROTOCOL.GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)  

[EFI\_BATTERY\_CHARGING\_PROTOCOL.GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)  

[EFI\_BATTERY\_CHARGING\_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)  
