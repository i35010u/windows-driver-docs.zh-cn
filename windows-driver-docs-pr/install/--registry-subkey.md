---
title: '* 注册表子项'
description: '* 注册表子项'
ms.assetid: 19b72c64-5a64-4655-b922-4a4bca162b32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f34b955081f2fd62faa72727f98bc5c74ca84755
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375769"
---
# <a name="-registry-subkey"></a>\* 注册表子项


从 Windows 7 开始**\\*** （星号） 注册表子项指定可移动设备功能重写应用于设备的所有节点 (*devnodes*) 设备枚举通过标识[HardwareID](hardwareid-registry-subkey.md)或[CompatibleID](compatibleid-registry-subkey.md)注册表子项。 重写有关可移动设备功能的详细信息，请参阅[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

**\\*** 注册表子项适用于通过指定的所有 devnodes 可移动设备功能重写**HardwareID**或**CompatibleID**基于规则的注册表子项[LocationPaths](locationpaths-registry-subkey.md)或[ChildLocationPaths](childlocationpaths-registry-subkey.md)对于重写指定的注册表子项。 例如，如果**\\*** 中指定的注册表子项**LocationPaths**子项，可移动设备功能覆盖应用到的设备标识的所有父 devnodes通过父**HardwareID**或**CompatibleID**注册表子项。

下表定义的格式和要求**\\*** 注册表子项。

| 注册表子项名称 | 必需/可选 | 格式要求 | 父子项                                                                                                      | 子级子项 |
|----------------------|-------------------|---------------------|--------------------------------------------------------------------------------------------------------------------|---------------|
| \*                   | 可选          | 无                | [LocationPaths](locationpaths-registry-subkey.md)或[ChildLocationPaths](childlocationpaths-registry-subkey.md) | 无          |

 

任一[LocationPath](locationpath-registry-subkey.md)或**\\*** 注册表子项必须存在以指示可移动设备功能的作用域重写。

\*注册表子项必须包含**可移动**DWORD 值，该值指定设备是否可移动。 下表定义的有效**可移动**值。

| 可移动的值 | 说明                                                 |
|-----------------|-------------------------------------------------------------|
| 0               | 适用 devnodes 应被认为是不可移除 |
| 1               | 应为可移动视为适用 devnodes     |

 

 

 





