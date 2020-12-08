---
title: EFI_DISPLAY_POWER_PROTOCOL
description: EFI_DISPLAY_POWER_PROTOCOL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 496cd5f53bec1579522d8b5b56ed44e0860268b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803405"
---
# <a name="efi_display_power_protocol"></a>EFI \_ 显示 \_ 电源 \_ 协议


此协议允许在 UEFI 环境中进行充电时，UEFI 电池充电应用程序在指定的空闲持续时间关闭屏幕。

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


<a href="" id="revision"></a>**A01**  
**EFI \_ 显示 \_ 电源 \_ 协议** 遵循的修订版本。 所有将来的修订版都必须是向后兼容。 如果未来版本不是向后兼容的，则必须使用不同的 GUID。

当前修订版本为0x00010000。 如果固件支持此版本的 **EFI \_ 电池 \_ 充电 \_ 协议** ，则修订号应设置为0x00010000。

<a href="" id="setdisplaypowerstate"></a>**SetDisplayPowerState**  
修改显示器和背光的电源状态。 有关详细信息，请参阅 [EFI \_ 显示 \_ 电源 \_ 协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)。

<a href="" id="getdisplaypowerstate"></a>**GetDisplayPowerState**  
返回显示器和背景光的当前电源状态。 有关详细信息，请参阅 [EFI \_ 显示 \_ 电源 \_ 协议。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




