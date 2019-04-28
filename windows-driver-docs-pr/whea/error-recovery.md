---
title: 错误恢复
description: 错误恢复
ms.assetid: 5710625f-bb65-41d4-a5c9-d61a48178859
keywords:
- Windows 硬件错误体系结构 WDK，错误恢复
- WHEA WDK，错误恢复
- 硬件错误 WDK WHEA，错误恢复
- 错误 WDK WHEA，错误恢复
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误恢复
- PSHED 插件 WDK WHEA 错误恢复
- 错误恢复 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19df39bf26e3bf061fb08d09a2e9d7b45d433e6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350591"
---
# <a name="error-recovery"></a>错误恢复


在可恢复的硬件错误的处理，操作系统将尝试从错误情况中恢复。 首先尝试从自己的错误条件恢复操作系统。 然后 PSHED 使它可以在执行从错误情况中恢复所需的任何硬件操作会调用 Windows 内核。 如果 PSHED 插件实现参与错误恢复，它是然后由调用 PSHED，以便它可以执行需要完全恢复的错误条件从任何其他特定于平台的硬件操作。 无论是否在操作系统已成功从自己的错误条件恢复，Windows 内核始终调用 PSHED 以确保 PSHED 和任何已注册的插件 PSHED 有机会更新或修改形式的硬件状态必需。

有关如何参与 PSHED 插件实现中错误恢复的详细信息，请参阅[参与错误恢复](participating-in-error-recovery.md)。

 

 




