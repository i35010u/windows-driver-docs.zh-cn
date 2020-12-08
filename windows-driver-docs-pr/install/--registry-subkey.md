---
title: '* 注册表子项'
description: '* 注册表子项'
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8bb71c609694fcc737ec3a14eaa473e5fe460dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826295"
---
# <a name="-registry-subkey"></a>\* 注册表子项


从 Windows 7 开始，* *\** _ (星号) 注册表子项指定可移动设备功能覆盖适用于所有设备节点 (_devnodes * ) 为通过 [HardwareID](hardwareid-registry-subkey.md) 或 [CompatibleID](compatibleid-registry-subkey.md) 注册表子项确定的设备枚举。 有关可移动设备功能替代的详细信息，请参阅 [DeviceOverrides 注册表项](deviceoverrides-registry-key.md)。

_ Registry 子项根据为替代指定的 [LocationPaths](locationpaths-registry-subkey.md)或 [ChildLocationPaths](childlocationpaths-registry-subkey.md)注册表子项的规则， **\* *将可移动设备功能重写应用于通过 _* HardwareID** 或 **CompatibleID** 注册表子项指定的所有 devnodes。 例如，如果 _ LocationPaths 子项 **\* *中指定了 _ 注册表子项*** ，则可移动设备功能覆盖适用于通过 parent **HardwareID** 或 **CompatibleID** registry 子项识别的设备的所有父 devnodes。

下表定义了 * _ 注册表子项的格式和要求 *\** 。

| 注册表子项名称 | 必需/可选 | 格式要求 | 父子项                                                                                                      | 子子项 |
|----------------------|-------------------|---------------------|--------------------------------------------------------------------------------------------------------------------|---------------|
| \_                   | 可选          | 无                | [LocationPaths](locationpaths-registry-subkey.md) 或 [ChildLocationPaths](childlocationpaths-registry-subkey.md) | 无          |

 

必须存在 [LocationPath](locationpath-registry-subkey.md) 或 * *\** _ 注册表子项，才能指示可移动设备功能覆盖的作用域。

\_注册表子项必须包含 **可移动** 的 DWORD 值，该值指定设备是否可移动。 下表定义了有效的 **可移动** 值。

| 可移动值 | 说明                                                 |
|-----------------|-------------------------------------------------------------|
| 0               | 适用的 devnodes 应视为不可删除 |
| 1               | 适用的 devnodes 应视为可移动     |
