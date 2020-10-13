---
title: 使用 "电源" 按钮强制系统崩溃
description: 使用 "电源" 按钮强制系统崩溃
keywords:
- 启动进程，导致 "系统崩溃" 按钮
- 系统崩溃，电源按钮
- bug 检查，电源按钮
ms.date: 10/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5ec612332170cdb5967870b6b61ddb956545abd1
ms.sourcegitcommit: 735fea11056fe943c4368ee54573790e0602de66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91979968"
---
# <a name="forcing-a-system-crash-with-the-power-button"></a>使用 "电源" 按钮强制系统崩溃

[Bug 检查0x1C8：](bug-check-0x1c8--manually-initiated-power-button-hold.md)如果设置以下注册表项，则可以强制执行手动系统崩溃 MANUALLY_INITIATED_POWER_BUTTON_HOLD：

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power]
"PowerButtonBugcheck"=dword:00000001
```

如果此注册表项 *不* 存在，则必须重新启动系统才能使此更改生效。

如果此 *注册表项存在* 并且更改了值，则系统 *无需重新* 启动即可使更改生效。

当电源按钮保留7秒钟，但在 UEFI 重置发生10秒之前已释放时，将发生 bug 检查。

若要支持长时间按钮保留，设备需要常规用途 i/o (GPIO) 的电源按钮、用于将电源事件路由到 Windows 电源管理器的固件和用于在注册表中启用 bug 检查功能的固件。

此功能在 Windows 10 1809/Windows Server 2019 和更高版本中可用。
