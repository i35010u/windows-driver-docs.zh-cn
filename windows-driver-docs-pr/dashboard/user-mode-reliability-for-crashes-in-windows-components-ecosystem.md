---
title: Windows 组件中用户模式可靠性的崩溃次数（按总体规范化）小于或等于基线目标
description: 该度量将 7 天滑动窗口中的遥测数据聚合为 Microsoft 组件在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率
ms.topic: article
ms.date: 08/08/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 50cb1ea0ec201003d53c368c1c3a4a9429144330
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223889"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-windows-components-photos-app-normalized-by-population-is-less-than-or-equal-to-the-baseline-goal"></a>Windows 组件照片应用中用户模式可靠性的崩溃次数（按总体规范化）小于或等于基线目标

## <a name="description"></a>描述

该度量监视 Windows 组件（例如 dwm.exe、shell、登录 UI 等）在显示器驱动程序中的崩溃频率（相对于使用该驱动程序的所有计算机数）。 如果 Windows 组件崩溃，用户必须先等待其恢复，然后才能再次使用它。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |生态系统|
|时间段 |7 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |10,000 台计算机|
|通过标准 |每 10,000 台计算机出现 15 次及以下次数的崩溃|
|度量 ID |20240811|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为由显卡驱动程序引起的 Windows 组件的崩溃比率（相对于使用该驱动程序的所有计算机） 
2. Windows 组件的崩溃总次数 = 计数（Windows 组件在使用该驱动程序的计算机上的崩溃次数） 
3. 设备总数 = 总和（使用该驱动程序的计算机数） 

### <a name="final-calculation"></a>最终计算 

4. 按设备计数规范化的 Windows 组件的崩溃次数 = Windows 组件的崩溃总次数 * 10,000/设备总数 
