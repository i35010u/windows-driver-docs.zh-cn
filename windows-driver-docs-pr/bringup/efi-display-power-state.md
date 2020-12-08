---
title: EFI_DISPLAY_POWER_STATE
description: EFI_DISPLAY_POWER_STATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f57552cd23006d04b4d06b518851ce35b470ca9b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789097"
---
# <a name="efi_display_power_state"></a>EFI \_ 显示 \_ 电源 \_ 状态


此枚举表示显示器和背光的充电状态。 此枚举是 [EFI \_ 显示 \_ 电源协议的参数 \_ 。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md) 和 [EFI \_ 显示 \_ 电源 \_ 协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md) 函数。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_DISPLAY_POWER_STATE {  
    EfiDisplayPowerStateUnknown = 0,  
    EfiDisplayPowerStateOff,  
    EfiDisplayPowerStateMaximum,  
} EFI_DISPLAY_POWER_STATE;
```

## <a name="elements"></a>元素


<a href="" id="efidisplaypowerstateunknown"></a>EfiDisplayPowerStateUnknown  
电源状态未初始化。 此值仅可用于变量初始化;不能将其传递到任何 [EFI \_ 显示 \_ 电源 \_ 协议](efi-display-power-protocol.md) 功能或由其返回。

<a href="" id="efidisplaypowerstateoff"></a>EfiDisplayPowerStateOff  
与 [EFI \_ 显示 \_ 电源协议一起使用时 \_ 。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)，表示显示和背景光的电源关闭。 与 [EFI \_ 显示 \_ 电源协议一起使用时 \_ 。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)，关闭显示屏和背光的电源。

<a href="" id="efidisplaypowerstatemaximum"></a>EfiDisplayPowerStateMaximum  
与 [EFI \_ 显示 \_ 电源协议一起使用时 \_ 。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)，表示显示和背景光具有完全功能。 与 [EFI \_ 显示 \_ 电源协议一起使用时 \_ 。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)，打开显示屏和背光的全部功能。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI \_ 显示 \_ 电源 \_ 协议](efi-display-power-protocol.md)  



