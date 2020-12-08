---
title: EFI_BATTERY_CHARGING_STATUS
description: EFI_BATTERY_CHARGING_STATUS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b626586f465ca6d73bb323edbca2c705c7658fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803409"
---
# <a name="efi_battery_charging_status"></a>EFI \_ 电池 \_ 充电 \_ 状态


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
操作已成功完成。

<a href="" id="efibatterychargingstatusoverheat"></a>EfiBatteryChargingStatusOverheat  
电池电量太热，无法充电。

<a href="" id="efibatterychargingstatusvoltageoutofrange"></a>EfiBatteryChargingStatusVoltageOutOfRange  
充电逻辑检测到电压超出操作范围。

<a href="" id="efibatterychargingstatuscurrentoutofrange"></a>EfiBatteryChargingStatusCurrentOutOfRange  
正在充电逻辑检测到当前要超出操作范围。

<a href="" id="efibatterychargingstatustimeout"></a>EfiBatteryChargingStatusTimeout  
充电逻辑检测到电池未在合理的时间内充电。

<a href="" id="efibatterychargingstatusaborted"></a>EfiBatteryChargingStatusAborted  
操作已中止。

<a href="" id="efibatterychargingstatusdeviceerror"></a>EfiBatteryChargingStatusDeviceError  
物理设备报告了一个错误。

<a href="" id="efibatterychargingstatusextremecold"></a>EfiBatteryChargingStatusExtremeCold  
电池太冷，无法继续充电。

<a href="" id="efibatterychargingstatusbatterychargingnotsupported"></a>EfiBatteryChargingStatusBatteryChargingNotSupported  
电池不支持充电操作。

<a href="" id="efibatterychargingstatusbatterynotdetected"></a>EfiBatteryChargingStatusBatteryNotDetected  
未检测到电池。

<a href="" id="efibatterychargingsourcenotdetected"></a>EfiBatteryChargingSourceNotDetected  
设备未连接到收费源，因此无法继续充电操作。

<a href="" id="eefibatterychargingsourcevoltageinvalid"></a>EEfiBatteryChargingSourceVoltageInvalid  
收费源提供的电压无效。

<a href="" id="efibatterychargingsourcecurrentinvalid"></a>EfiBatteryChargingSourceCurrentInvalid  
收费源提供了无效的电流。

<a href="" id="efibatterychargingerrorrequestshutdown"></a>EfiBatteryChargingErrorRequestShutdown  
驱动程序请求系统关闭。

<a href="" id="efibatterychargingerrorrequestreboot"></a>EfiBatteryChargingErrorRequestReboot  
驱动程序请求系统重新启动。

## <a name="remarks"></a>备注


Efi \_ 电池 \_ 充电 \_ 状态在 [efi \_ 电池 \_ 充电 \_ 完成 \_ 标记](efi-battery-charging-completion-token.md)结构的 **状态** 成员中返回。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI \_ 电池 \_ 充电 \_ 完成 \_ 令牌](efi-battery-charging-completion-token.md)  



