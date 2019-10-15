---
title: '* 注册表子项'
description: '* 注册表子项'
ms.assetid: 19b72c64-5a64-4655-b922-4a4bca162b32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 992657e051c8896d383dc906b01f52d9d733f4f2
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038098"
---
# <a name="-registry-subkey"></a>\* 注册表子项


从 Windows 7 开始， **\*** （星号）注册表子项指定可移动设备功能覆盖适用于为通过[HardwareID 或](hardwareid-registry-subkey.md)标识的设备枚举的所有设备节点（*devnodes*）[CompatibleID](compatibleid-registry-subkey.md)注册表子项。 有关可移动设备功能替代的详细信息，请参阅[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

\* 注册表子项会将可移动设备功能重写应用于通过HardwareID或CompatibleID注册表子项指定的所有 devnodes，具体取决于[LocationPaths](locationpaths-registry-subkey.md)的规则或为替代指定的 [ChildLocationPaths](childlocationpaths-registry-subkey.md) 注册表子项。 例如，如果在**LocationPaths**子项中指定了 **\*** 注册表子项，则可移动设备功能覆盖适用于通过父**HardwareID**标识的设备的所有父 devnodes 或**CompatibleID**注册表子项。

下表定义 **\*** 注册表子项的格式和要求。

| 注册表子项名称 | 必需/可选 | 格式要求 | 父子项                                                                                                      | 子子项 |
|----------------------|-------------------|---------------------|--------------------------------------------------------------------------------------------------------------------|---------------|
| \*                   | 可选          | 无                | [LocationPaths](locationpaths-registry-subkey.md)或[ChildLocationPaths](childlocationpaths-registry-subkey.md) | 无          |

 

必须存在[LocationPath](locationpath-registry-subkey.md)或 **\*** 注册表子项，才能指示可移动设备功能重写的作用域。

@No__t-0 注册表子项必须包含一个**可移动**DWORD 值，该值指定设备是否可移动。 下表定义了有效的**可移动**值。

| 可移动值 | 说明                                                 |
|-----------------|-------------------------------------------------------------|
| 0               | 适用的 devnodes 应视为不可删除 |
| 1               | 适用的 devnodes 应视为可移动     |
