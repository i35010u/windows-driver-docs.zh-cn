---
title: 预计故障分析 (PFA)
description: 预计故障分析 (PFA)
ms.assetid: d2ded330-edcc-4bdd-9b52-73c1961d8ef2
keywords:
- Windows 硬件错误体系结构 WDK，预计故障分析
- Windows 硬件错误体系结构 WDK PFA
- WHEA WDK，预计故障分析
- WHEA WDK PFA
- 预计故障分析 (PFA) WDK WHEA
- PFA WDK WHEA
- 故障分析 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aa20c31aa995cc3b23d6c242d5b486249beb650
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340739"
---
# <a name="predictive-failure-analysis-pfa"></a>预计故障分析 (PFA)


Windows 硬件错误体系结构 (WHEA) 支持 ECC 内存用于预测故障分析 (PFA)。 通过使用 PFA，WHEA 可以监视遇到以前的错误的一个或多个 ECC 内存页。 如果错误数超过可配置的时间间隔内的同一页的阈值，WHEA 会尝试将内存页脱机。

计算机系统，尤其是服务器系统，通常配备有自动更正特定类型的内存错误的错误更正代码 (ECC) 内存。 在系统中具有 ECC 内存，已更正的错误和它们的频率信息可供操作系统，并且可以用于预测即将发生故障，包括了无法纠正可能导致非计划停机时间和发生灾难性的故障.

通过使用注册表设置，可以为 WHEA 配置 PFA 错误阈值、 时间间隔和其他参数。 有关如何执行此操作的详细信息，请参阅[WHEA 策略设置](whea-pfa-registry-settings.md)。

WHEA PFA 的执行方式的概述，请参阅[PFA 由 WHEA](pfa-performed-by-whea.md)。

一个[特定于平台的硬件错误驱动程序 (PSHED) 插件驱动程序](platform-specific-hardware-error-driver-plug-ins2.md)还可以执行 PFA ECC 内存。 这种方式，该插件 (而不是 WHEA) 必须监视 ECC 内存页。 有关如何 PSHED 插件执行 PFA 详细信息，请参阅[PFA 由 PSHED 插件](pfa-performed-by-a-pshed-plug-in.md)。

当 PFA 预测 ECC 内存页将会失败时，从而节省了 (或*仍然存在*) 引导配置数据 (BCD) 系统存储区中的结果。 有关此过程的详细信息，请参阅[PFA 结果持久性](persistence-of-pfa-results.md)。

WHEA 在 Windows 7 和更高版本的 Windows 上支持 PFA。

 

 




