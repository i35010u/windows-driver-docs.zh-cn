---
title: 检测驱动程序加载错误
description: 检测驱动程序加载错误
keywords:
- 驱动程序加载错误 WDK 驱动程序签名
- 错误 WDK 驱动程序签名
- 检测驱动程序已加载
- 加载错误 WDK 驱动程序签名
- 状态信息 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a123de79d41742a50044eb08c6e308be397cbe06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827751"
---
# <a name="detecting-driver-load-errors"></a>检测驱动程序加载错误


若要检测驱动程序是否已加载，请在设备管理器中检查设备的状态。 如果 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 阻止驱动程序加载，因为驱动程序未正确签名，则设备状态消息将指示 Windows 无法加载驱动程序，并且驱动程序可能已损坏或丢失。 如果出现这种情况，你可以使用 [代码完整性诊断系统日志事件](code-integrity-diagnostic-system-log-events.md) 来进一步诊断问题。 有关代码52的详细信息，请参阅 [CM_PROB_UNSIGNED_DRIVER](cm-prob-unsigned-driver.md)。

有关设备管理器报告的错误的完整列表，请参阅 [设备管理器错误消息](device-manager-error-messages.md)。

有关可帮助解决问题的其他信息，请参阅 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)。

