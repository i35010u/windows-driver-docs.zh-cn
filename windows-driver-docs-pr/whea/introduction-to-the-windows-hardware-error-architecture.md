---
title: Windows 硬件错误体系结构 (WHEA) 简介
description: Windows 硬件错误体系结构 (WHEA) 简介
ms.assetid: 5a0bbf8c-d644-4a64-9a7e-400d5de2c8fa
keywords:
- Windows 硬件错误体系结构 WDK，有关 Windows 硬件错误体系结构
- WHEA WDK，有关 Windows 硬件错误体系结构
- 硬件错误 WDK WHEA，有关 Windows 硬件错误体系结构
- 错误 WDK WHEA，有关 Windows 硬件错误体系结构
- 源信息 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e566a3c14b9ab758a26f09b7ef8766b47f1a30f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340777"
---
# <a name="introduction-to-the-windows-hardware-error-architecture"></a>Windows 硬件错误体系结构简介


在 Windows Vista 之前的 Microsoft Windows 操作系统版本中，操作系统支持多个不相关的机制报告硬件错误。 这些机制进行错误恢复提供极少的支持。 对于未更正错误，操作系统只是生成的 bug 检查，然后将一些用错误的信息系统事件日志中记录后重新启动系统。

确定硬件错误的根本原因的能力是有限数量的系统事件日志中记录的错误信息影响。 操作系统无法阻止系统崩溃，因为没有任何常见硬件错误引起的错误记录格式和硬件错误管理应用程序的支持却很少。

Windows 硬件错误体系结构 (WHEA)，与 Windows Vista 引入了扩展以前的硬件错误报告机制，并使它们一起作为连贯的硬件错误基础结构的组件。 WHEA 利用的额外的硬件错误信息可在今天的硬件设备，并与系统固件得更紧密地集成。

因此，WHEA 提供以下优势：

-   允许更多的错误数据将变得可用于确定硬件错误的根本原因的标准错误记录格式。

-   提供了机制来帮助恢复从硬件错误，以避免导致 bug 检查非致命硬件错误时。

-   支持用户模式错误管理应用程序并启用高级的系统运行状况监视通过事件跟踪 Windows (ETW) 事件和错误管理和控制提供了一个 API。

-   提供可扩展性，使 WHEA 硬件供应商添加新的和更好的硬件错误报告到他们的设备的机制，允许操作系统以适当地适应新的机制。

 

 




