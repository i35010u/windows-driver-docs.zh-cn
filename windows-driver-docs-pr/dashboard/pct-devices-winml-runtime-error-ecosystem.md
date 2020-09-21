---
title: 遇到 WinML 运行时错误的设备所占的百分比（生态系统）
description: 该度量监视 Windows 机器学习的总体运行状况和可靠性（生态系统）
ms.topic: article
ms.date: 4/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7e649e83934c52a61a7b0402091dcc65e68a1030
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101716"
---
# <a name="percent-of-devices-with-winml-runtime-error-ecosystem"></a>遇到 WinML 运行时错误的设备所占的百分比（生态系统）

## <a name="description"></a>说明

这是一种生态系统度量，用于监视 Windows 机器学习中 GPU 执行路径的总体运行状况和可靠性。 它通过使用 WinML RuntimeError 遥测和 WinML SessionCreation 遥测来跟踪出现 WinML RuntimeError 的设备所占的百分比。

此度量将计算使用 GPU 会话运行 WinML 且出现 WinML RuntimeError 的设备所占的百分比。 WinML 具有 CPU 和 GPU 执行路径。 此度量仅考虑来自 GPU 路径的结果。

这与[出现 WinML 运行时错误的设备所占的百分比](./pct-devices-winml-runtime-error.md)的生态系统相对应，这意味着它将包含多个面向同一驱动程序版本的驱动程序外部测试版中的数据。 之所以要采用驱动程序生态系统度量，是因为我们希望标准 WinML 驱动程序外部测试版度量仅包含少量数据。 一旦驱动程序外部测试版度量不满足最低数据要求，我们将使用此生态系统度量制定决策。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|生态系统|
|时间段 |30 天|
|度量标准 |计算机|
|最小总体数量 |30 台设备，使用置信区间|
|通过标准 |小于 1%|
|度量 ID |27057557|

## <a name="calculation"></a>计算

我们将运行时错误聚合到设备级别，然后计算出现运行时错误的设备所占的百分比。 计算的粒度基于每天。

度量值 = COUNT（出现运行时错误的设备总数）/COUNT（设备总数）