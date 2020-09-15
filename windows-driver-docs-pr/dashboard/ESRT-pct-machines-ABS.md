---
title: 异常关机并非由于 Bug 检查或电源按钮原因的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为一个比率，即安装后 3 天内报告了异常关机的计算机数/成功安装的计算机数
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 49c7bad04236ad7e6894beaf5c88fd1f6fbe45fa
ms.sourcegitcommit: c214e65a7f5dd868037718a34ca7cc80584df5c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89615467"
---
# <a name="percent-of-machines-with-abnormal-shutdown-not-due-to-bugcheck-or-power-button"></a>异常关机并非由于 Bug 检查或电源按钮原因的计算机的百分比

## <a name="description"></a>说明

安装成功的计算机的百分比，此类计算机在安装后 3 天内出现的异常关机并非由于 Bug 检查（此检查会自动触发 ABS），也不是由于电源按钮导致的不正常关机，而且此类计算机在安装之前的 3 天没有异常关机。

该度量将 28 天滑动窗口中的遥测数据聚合为一个比率，即安装后 3 天内报告了异常关机的计算机数/成功安装的计算机数

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |250|
|通过标准 |<= 20%|
|度量 ID |20431908 或 23260722|

## <a name="calculation"></a>计算

在成功安装（由度量 20116729 定义）后 3 天内报告了异常关机且安装前的 3 天没有触发 ABS 的计算机数/

成功安装的计算机数

