---
title: EFI_DISPLAY_POWER_STATE
description: EFI_DISPLAY_POWER_STATE
ms.assetid: b4b0980b-db87-44e8-842c-afce0c8df0a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2a9230c4286efe8a39a2a3f7fdbee8c2a8cf327
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328008"
---
# <a name="efidisplaypowerstate"></a>EFI\_DISPLAY\_POWER\_STATE


此枚举表示显示和背景光的充电的状态。 此枚举是一个参数的[EFI\_显示\_POWER\_协议。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)并[EFI\_显示\_POWER\_协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)函数。

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
未初始化的电源状态。 此值仅可用于变量初始化;无法传递给或任何返回的[EFI\_显示\_POWER\_协议](efi-display-power-protocol.md)函数。

<a href="" id="efidisplaypowerstateoff"></a>EfiDisplayPowerStateOff  
与一起使用时[EFI\_显示\_POWER\_协议。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)，指示来显示和背景光电源已关闭。 与一起使用时[EFI\_显示\_POWER\_协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)、 显示和背景光电源关闭。

<a href="" id="efidisplaypowerstatemaximum"></a>EfiDisplayPowerStateMaximum  
与一起使用时[EFI\_显示\_POWER\_协议。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)，指示的显示和背景光具有完整功能。 与一起使用时[EFI\_显示\_POWER\_协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)、 打开来显示和背景光的全部功能。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI\_DISPLAY\_电源\_协议](efi-display-power-protocol.md)  



