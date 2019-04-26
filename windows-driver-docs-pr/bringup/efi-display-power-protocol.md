---
title: EFI_DISPLAY_POWER_PROTOCOL
description: EFI_DISPLAY_POWER_PROTOCOL
ms.assetid: 61ccf856-7e0b-4f1b-9be9-7b8a31339a6b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 646406e0af3a813e986c3d804f64f279bff9f668
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328015"
---
# <a name="efidisplaypowerprotocol"></a>EFI\_DISPLAY\_电源\_协议


此协议允许 UEFI 电池充电时充电 UEFI 环境中指定的空闲时间后关闭屏幕的应用程序。

## <a name="syntax"></a>语法


```cpp
#define EFI_DISPLAY_POWER_PROTOCOL_GUID \
  {0xf352021d, 0x9593, 0x4432, {0xbf, 0x4, 0x67, 0xb9, 0xf3, 0xb7, 0x60, 0x8};

typedef struct _EFI_DISPLAY_POWER_PROTOCOL {  
    UINT32                                    Revision;  
    EFI_DISPLAY_POWER_SETDISPLAYPOWERSTATE    SetDisplayPowerState;  
    EFI_DISPLAY_POWER_GETDISPLAYPOWERSTATE    GetDisplayPowerState;  
} EFI_DISPLAY_POWER_PROTOCOL;
```

## <a name="members"></a>成员


<a href="" id="revision"></a>**修订版本**  
修订**EFI\_显示\_POWER\_协议**遵循。 所有未来的版本必须是向后兼容。 如果将来的版本不是向后兼容，必须使用不同的 GUID。

当前的修订版本是 0x00010000。 修订版本应设置为 0x00010000 固件如果此的修订版**EFI\_电池\_正在充电\_协议**固件支持。

<a href="" id="setdisplaypowerstate"></a>**SetDisplayPowerState**  
修改显示和背景光电源的状态。 有关详细信息，请参阅[EFI\_显示\_POWER\_协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)。

<a href="" id="getdisplaypowerstate"></a>**GetDisplayPowerState**  
返回当前的显示和背景光电源状态。 有关详细信息，请参阅[EFI\_显示\_POWER\_协议。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




