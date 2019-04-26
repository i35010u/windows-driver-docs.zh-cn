---
title: EFI_BATTERY_CHARGING_STATUS
description: EFI_BATTERY_CHARGING_STATUS
ms.assetid: dc267920-2c2f-447b-8772-35160886a24c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e9ff65fbcdf645d5617409dda1c05daec26f12f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328019"
---
# <a name="efibatterychargingstatus"></a>EFI\_电池\_正在充电\_状态


此枚举指定充电电池的状态。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_BATTERY_CHARGING_STATUS {      
    EfiBatteryChargingStatusNone = 0,
    EfiBatteryChargingStatusSuccess,
    EfiBatteryChargingStatusOverheat,
    EfiBatteryChargingStatusVoltageOutOfRange,
    EfiBatteryChargingStatusCurrentOutOfRange,
    EfiBatteryChargingStatusTimeout,
    EfiBatteryChargingStatusAborted,
    EfiBatteryChargingStatusDeviceError,
    EfiBatteryChargingStatusExtremeCold,
    EfiBatteryChargingStatusBatteryChargingNotSupported,
    EfiBatteryChargingStatusBatteryNotDetected,
    EfiBatteryChargingSourceNotDetected,
    EfiBatteryChargingSourceVoltageInvalid,
    EfiBatteryChargingSourceCurrentInvalid,
    EfiBatteryChargingErrorRequestShutdown,
    EfiBatteryChargingErrorRequestReboot
} EFI_BATTERY_CHARGING_STATUS;
```

## <a name="elements"></a>元素


<a href="" id="efibatterychargingstatusnone"></a>EfiBatteryChargingStatusNone  
充电状态不可用。

<a href="" id="efibatterychargingstatussuccess"></a>EfiBatteryChargingStatusSuccess  
已成功完成该操作。

<a href="" id="efibatterychargingstatusoverheat"></a>EfiBatteryChargingStatusOverheat  
电池正在充电温度过高。

<a href="" id="efibatterychargingstatusvoltageoutofrange"></a>EfiBatteryChargingStatusVoltageOutOfRange  
收费逻辑检测到电压超出操作的范围为。

<a href="" id="efibatterychargingstatuscurrentoutofrange"></a>EfiBatteryChargingStatusCurrentOutOfRange  
收费逻辑检测到当前要超出操作的范围。

<a href="" id="efibatterychargingstatustimeout"></a>EfiBatteryChargingStatusTimeout  
收费逻辑检测到电池不被收费合理时间内。

<a href="" id="efibatterychargingstatusaborted"></a>EfiBatteryChargingStatusAborted  
操作已中止。

<a href="" id="efibatterychargingstatusdeviceerror"></a>EfiBatteryChargingStatusDeviceError  
物理设备报告了错误。

<a href="" id="efibatterychargingstatusextremecold"></a>EfiBatteryChargingStatusExtremeCold  
电池是太冷，若要继续收费。

<a href="" id="efibatterychargingstatusbatterychargingnotsupported"></a>EfiBatteryChargingStatusBatteryChargingNotSupported  
电池不支持的计费操作。

<a href="" id="efibatterychargingstatusbatterynotdetected"></a>EfiBatteryChargingStatusBatteryNotDetected  
未检测到电池。

<a href="" id="efibatterychargingsourcenotdetected"></a>EfiBatteryChargingSourceNotDetected  
设备未连接到充电源，因此无法继续与计费操作。

<a href="" id="eefibatterychargingsourcevoltageinvalid"></a>EEfiBatteryChargingSourceVoltageInvalid  
充电源提供无效的电压。

<a href="" id="efibatterychargingsourcecurrentinvalid"></a>EfiBatteryChargingSourceCurrentInvalid  
提供无效的当前计费的源。

<a href="" id="efibatterychargingerrorrequestshutdown"></a>EfiBatteryChargingErrorRequestShutdown  
该驱动程序请求了系统关闭。

<a href="" id="efibatterychargingerrorrequestreboot"></a>EfiBatteryChargingErrorRequestReboot  
该驱动程序请求的系统重启。

## <a name="remarks"></a>备注


EFI\_电池\_正在充电\_中返回状态**状态**隶属[EFI\_电池\_正在充电\_完成\_令牌](efi-battery-charging-completion-token.md)结构。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI\_电池\_正在充电\_完成\_令牌](efi-battery-charging-completion-token.md)  



