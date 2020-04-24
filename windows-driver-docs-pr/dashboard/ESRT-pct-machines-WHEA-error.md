---
title: 固件安装后出现 WHEA 错误的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为报告了致命 WHEA 事件的计算机数与成功安装固件的计算机数的比率
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7c9b46519daeb40725267ac9d285a1442bfd611b
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "79083124"
---
# <a name="percent-of-machines-with-windows-hardware-error-architecture-whea-error-after-firmware-installation"></a>固件安装后出现 Windows 硬件错误体系结构 (WHEA) 错误的计算机的百分比

## <a name="description"></a>说明

在成功安装固件后报告了致命 WHEA 事件 (WheaProvider.WheaDriverErrorExternal) 的计算机的百分比。

该度量将 28 天滑动窗口中的遥测数据聚合为报告了致命 WHEA 事件的计算机数与成功安装固件的计算机数的比率

WHEA 事件仅在 20H1 生成中检索到，很快会后向移植到 19H1。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |200|
|通过标准 |<= 5%|
|度量 ID |20319726|

## <a name="calculation"></a>计算

报告了致命 WHEA 错误的计算机数/

成功安装固件的计算机数（由度量 20116729 定义）

