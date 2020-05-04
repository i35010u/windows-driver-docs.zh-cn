---
title: 指纹登录体验的成功率
description: 该度量跟踪使用指纹传感器登录的用户体验。
ms.topic: article
ms.date: 03/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5af92b66d92d6032a1d97952d34cd784206c6aa4
ms.sourcegitcommit: 774d42aa3392ae88f4890d901dbd3e8945cb2658
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82139491"
---
# <a name="success-rate-of-fingerprint-sign-in-experience"></a>指纹登录体验的成功率

## <a name="description"></a>说明 

当用户已在 Windows Hello 中注册了指纹时，一个凭据提供程序将会枚举到锁屏界面上，以捕获用户的指纹手势。 如果用户触摸其传感器，一个样本将被收集并与设备上注册的指纹模板进行比较。 如果在解锁会话中有三次尝试，并且其中收集的样本与注册的模板不匹配，则指纹将被暂时锁定，直到用户使用其他凭据解锁。 如果生物识别传感器出现故障，则用户也会被阻止使用它进行解锁。 

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |7 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |50|
|通过标准 |>= 90%|
|度量 ID |19554065|

## <a name="calculation"></a>计算

1. 此度量聚合了 7 天滑动窗口中的遥测数据。
2. 指纹登录体验的成功率是在该窗口中按每台计算机计算的。
    1. 如果设备上的用户已注册指纹，则每个解锁会话都将从指纹凭据提供程序生成一个事件以及一个结果。 
    2. 具有特定良性结果的会话将被筛选出来。 以下情况会被筛选掉：
        1. NoFPEnrollments - 登录的用户未注册指纹。
        2. BUMissingNoEnrollments - 生物识别框架未枚举指纹传感器，并且用户无指纹注册。 
        3. BioDeviceNotAttached - 没有任何 FP 传感器连接到计算机。 这适用于使用外部的可移动传感器的情况。
        4. NoFPLogonAttempts - 用户未尝试使用指纹登录，并已使用另一个凭据提供程序进行登录。
        5. TriedFPUsedOtherProvider - 用户尝试了指纹，但使用了其他凭据提供程序进行登录。 用户未锁定指纹凭据提供程序。
    3. 成功会话数将除以剩余会话总数。 
3. 平均值是针对所有计算机上的成功率计算的。

## <a name="final-calculation"></a>最终计算
指纹登录成功率 = average(所有实例)