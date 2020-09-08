---
title: 遇到 WinML 运行时错误的设备所占的百分比
description: 该度量监视 Windows 机器学习的总体运行状况和可靠性
ms.topic: article
ms.date: 8/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9c0b3f90871f46f2c2fee41b2f53a3e4962139fd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183919"
---
# <a name="percent-of-devices-with-winml-runtime-error"></a>遇到 WinML 运行时错误的设备所占的百分比

## <a name="description"></a>说明

此度量监视 Windows 机器学习功能的总体运行状况和可靠性。

此度量的主要用途是跟踪遇到 Winml 运行时错误的设备所占的百分比。

该度量仅使用 WinML 运行时错误遥测和 WinML SessionCreation 遥测。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |标准|
|时间段 |30 天|
|度量标准 |计算机|
|最小总体数量 |30 台设备，使用置信区间|
|通过标准 |小于 1%|
|度量 ID |25419759|

## <a name="calculation"></a>计算

使用遇到 winml 运行时错误的每日不同设备计数除以使用了 winml 的每日不同设备计数

度量值 = 发送了 Winml 运行时错误遥测数据的每日不同 DeviceId 计数/发送了 Winml ProcessInfo 遥测数据的每日不同 DeviceId 计数
