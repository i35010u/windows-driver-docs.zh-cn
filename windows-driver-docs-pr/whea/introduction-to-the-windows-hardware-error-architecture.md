---
title: 'Windows 硬件错误体系结构简介 (WHEA) '
description: 'Windows 硬件错误体系结构简介 (WHEA) '
keywords:
- Windows 硬件错误体系结构 WDK，关于 Windows 硬件错误体系结构
- WHEA WDK，关于 Windows 硬件错误体系结构
- 硬件错误 WDK WHEA，关于 Windows 硬件错误体系结构
- 错误 WDK WHEA，关于 Windows 硬件错误体系结构
- 源信息 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d252fff3b21b04716c094be8d58f216ccd14f864
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787125"
---
# <a name="introduction-to-the-windows-hardware-error-architecture"></a>Windows 硬件错误体系结构简介

Windows Vista 中引入的 Windows 硬件错误体系结构 (WHEA) ，它扩展了以前的硬件错误报告机制，并将它们组合成了一个连贯的硬件错误基础结构的组件。 WHEA 利用当今硬件设备中提供的其他硬件错误信息，并与系统固件紧密集成。

因此，WHEA 具有以下优势：

-   允许以标准错误记录格式提供更广泛的错误数据，以便确定硬件错误的根本原因。

-   提供有助于从硬件错误中恢复的机制，以避免在硬件错误不严重时导致 bug 检查。

-   支持用户模式错误管理应用程序，并通过 Windows (ETW) 事件的事件跟踪以及提供用于错误管理和控制的 API 来启用高级系统运行状况监视。

-   提供可扩展性，因此，在硬件供应商向其设备添加新的和更好的硬件错误报告机制时，WHEA 允许操作系统适应新的机制。

