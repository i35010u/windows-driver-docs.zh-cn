---
title: 显卡驱动程序二进制文件中的崩溃导致发生了 TDR 的计算机数
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同的计算机，这些计算机由于显卡驱动程序二进制文件中的崩溃而发生了 TDR
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 8a955bd25907960c7ed8e4d89c131db4bf840d45
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223957"
---
# <a name="number-of-machines-that-had-a-tdr-caused-by-a-crash-in-the-graphics-driver-binary"></a>显卡驱动程序二进制文件中的崩溃导致发生了 TDR 的计算机数

## <a name="description"></a>描述

在用户会话期间，显卡驱动程序二进制文件中的崩溃会导致计算机的屏幕挂起或完全冻结。 超时检测和恢复 (TDR) 事件会尝试检测这些挂起，并动态恢复以取消冻结显示器。 遇到 TDR 的用户在 TDR 成功之前将无法使用计算机，这会导致屏幕闪烁。 

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |展开|
|时间段 |7 天滑动窗口|
|度量标准 |计算机的聚合|
|最小总体数量 |10,000|
|通过标准 |<= 130/10,000 台计算机遇到 TDR|
|度量 ID |20574707|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同的计算机，这些计算机由于显卡驱动程序二进制文件中的崩溃而发生了 TDR（相对于总体）   。
2. 发生 TDR 的计算机数 = 计数（驱动程序具有 TDR 的计算机） 
3. 计算机总数 = 计数（使用该驱动程序的计算机数） 
4. 发生 TDR 的计算机的比率 = 发生 TDR 的计算机数/计算机总数 

### <a name="final-calculation"></a>最终计算

5. 命中 TDR 的计算机数 = 发生 TDR 的计算机的比率 * 10,000 
6. 结果规范化为 10,000 台计算机，最终计算为：  

   i. [命中 TDR 的计算机数] 10,000 台计算机中由于显卡驱动程序二进制文件中的崩溃而遇到蓝屏的不同的计算机数