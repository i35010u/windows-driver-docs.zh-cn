---
title: 预计故障分析 (PFA)
description: 预计故障分析 (PFA)
keywords:
- Windows 硬件错误体系结构 WDK、预测性故障分析
- Windows 硬件错误体系结构 WDK，PFA
- WHEA WDK，预测故障分析
- WHEA WDK，PFA
- 预测性故障分析 (PFA) WDK WHEA
- PFA WDK WHEA
- 失败分析 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 983c2745ffae418931a1475538530e83f48ab7f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834823"
---
# <a name="predictive-failure-analysis-pfa"></a>预计故障分析 (PFA)


Windows 硬件错误体系结构 (WHEA) 支持 ECC 内存 (PFA) 的预测性故障分析。 通过使用 PFA，WHEA 可以监视一个或多个已遇到以前错误的 ECC 内存页。 如果错误数在可配置的时间间隔内超出同一页面的阈值，则 WHEA 会尝试使内存页脱机。

计算机系统（尤其是服务器系统）通常配备错误更正代码 (ECC) 内存，可自动更正特定类型的内存错误。 在具有 ECC 内存的系统中，有关已更正错误及其频率的信息可用于操作系统，并可用于预测即将发生的故障，包括可能会造成灾难性故障并导致计划外停机的无法纠正的故障。

你可以使用注册表设置来配置 WHEA 的 PFA 错误阈值、时间间隔和其他参数。 有关如何执行此操作的详细信息，请参阅 [WHEA 策略设置](whea-pfa-registry-settings.md)。

有关 WHEA 如何执行 PFA 的概述，请参阅 [WHEA 执行的 PFA](pfa-performed-by-whea.md)。

[ (PSHED) 插件驱动程序的特定于平台的硬件错误驱动程序](platform-specific-hardware-error-driver-plug-ins2.md)还可以在 ECC 内存上执行 PFA。 这样，插件 (不 WHEA) 必须监视 ECC 内存页。 有关 PSHED 插件如何执行 PFA 的详细信息，请参阅 [PSHED 插件执行的 PFA](pfa-performed-by-a-pshed-plug-in.md)。

当 PFA 预测 ECC 内存页将失败时，它会将 (或 *保留*) 引导配置数据 (BCD) 系统存储中的结果。 有关此过程的详细信息，请参阅 [PFA 结果的暂留](persistence-of-pfa-results.md)。

WHEA 在 Windows 7 和更高版本的 Windows 上支持 PFA。

 

 




