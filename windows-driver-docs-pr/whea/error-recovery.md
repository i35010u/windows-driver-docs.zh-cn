---
title: 错误恢复
description: 错误恢复
keywords:
- Windows 硬件错误体系结构 WDK，错误恢复
- WHEA WDK，错误恢复
- 硬件错误 WDK WHEA，错误恢复
- 错误 WDK WHEA，错误恢复
- 平台特定硬件错误驱动程序插件 WDK WHEA，错误恢复
- PSHED 插件 WDK WHEA，错误恢复
- 错误恢复 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2317c0bac68b6dcd491f4ca71a7e48a26cdc86a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824801"
---
# <a name="error-recovery"></a>错误恢复


在对可恢复的硬件错误进行处理的过程中，操作系统会尝试从错误情况中恢复。 首先，操作系统会自行尝试从错误条件恢复。 然后，Windows 内核会调入 PSHED，为其提供执行从错误情况恢复所需的任何硬件操作的机会。 如果实现了参与错误恢复的 PSHED 插件，则 PSHED 会调用它，以便它可以执行从错误条件完全恢复所需的任何其他特定于平台的硬件操作。 无论操作系统是否成功从错误条件恢复，Windows 内核都将始终调用 PSHED，以确保 PSHED 和任何已注册的 PSHED 插件有机会根据需要更新或修改硬件状态。

有关如何实现参与错误恢复的 PSHED 插件的详细信息，请参阅 [参与错误恢复](participating-in-error-recovery.md)。

 

 




