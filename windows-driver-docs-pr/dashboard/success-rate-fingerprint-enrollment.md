---
title: 指纹注册的成功率
description: 该度量查看经历整个注册体验的成功情况
ms.topic: article
ms.date: 03/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: c5bdb45a420586623eac3bef0e73468ac487c48f
ms.sourcegitcommit: 774d42aa3392ae88f4890d901dbd3e8945cb2658
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82139493"
---
# <a name="success-rate-of-fingerprint-enrollment"></a>指纹注册的成功率

## <a name="description"></a>说明 

如果用户的指纹传感器已连接到其设备上，则会向用户提供该传感器以注册其指纹，从而将其指纹用作解锁手势。 注册体验将在 Windows 全新体验中启动，也可以从设置启动。 此度量监视完成该体验的成功率。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小实例数 |10|
|通过标准 |>= 90%|
|度量 ID |22162022|

## <a name="calculation"></a>计算

1.  此度量将来自 7 天滑动窗口的遥测数据聚合为设备成功完成指纹注册的实例所占的百分比。 
2.  如果用户启动指纹注册应用程序，并且能够将模板提交给生物识别数据库，那么这就是一次成功。
3.  失败是任何导致注册失败的灾难性错误，包括生物识别传感器故障。
4.  会从实例池筛选掉用户启动的注册应用程序取消。 

## <a name="final-calculation"></a>最终计算
指纹注册成功率 = 成功的注册实例/所有实例
