---
title: EFI_BATTERY_CHARGING_PROTOCOL
description: EFI_BATTERY_CHARGING_PROTOCOL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f04948ddf39b6597e487e1bbf3b5a0b97ac59f32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803415"
---
# <a name="efi_battery_charging_protocol"></a>EFI \_ 电池 \_ 充电 \_ 协议


此协议允许 UEFI 驱动程序支持对主电池充电。

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
使用指定的最大电流向指定级别的主电池收费。

<a href="" id="revision"></a>**A01**  
EFI \_ 电池 \_ 充电协议遵从的修订版本 \_ 。 所有将来的修订版都必须是向后兼容。 如果未来版本不是向后兼容的，则必须使用不同的 GUID。

当前修订版本为0x00010002，但也支持修订版0x00010001。 有关每个协议版本支持的功能的详细信息，请参阅下面的 "备注" 部分。

<a href="" id="getbatteryinformation"></a>**GetBatteryInformation**  
返回有关主电池的当前状态的信息。 此函数类似于 **GetBatteryStatus**，但它提供了比 **GetBatteryStatus** 更多的信息。

## <a name="remarks"></a>备注


下表列出了 EFI \_ 电池 \_ 充电协议协议的每个版本支持的功能 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>修订0x00010002</th>
<th>修订0x00010001</th>
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

[EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)  

[EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)  

[EFI \_ 电池 \_ 充电 \_ 协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)  
