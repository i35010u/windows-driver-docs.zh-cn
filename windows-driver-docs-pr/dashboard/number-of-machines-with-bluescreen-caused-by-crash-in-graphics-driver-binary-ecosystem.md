---
title: 显卡驱动程序二进制文件中的崩溃导致出现蓝屏的计算机数
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同的计算机，这些计算机由于显卡驱动程序二进制文件中的崩溃而发生了蓝屏
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 65af3502ff091cf8712f92822797ee5e33a7856a
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016964"
---
# <a name="number-of-machines-with-a-blue-screen-caused-by-a-crash-in-graphics-driver-binary"></a>显卡驱动程序二进制文件中的崩溃导致出现蓝屏的计算机数

## <a name="description"></a>描述

在用户会话期间，显卡驱动程序二进制文件中的崩溃将导致蓝屏，这会重启计算机，并且可能会中断用户的工作流。 该度量评估使用给定驱动程序版本且因显卡驱动程序二进制文件中的崩溃而导致蓝屏的计算机数（相对于总体）。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |生态系统|
|时间段 |7 天滑动窗口|
|度量标准 |计算机的聚合|
|最小总体数量 |120,000 台计算机|
|通过标准 |<= 30/10,000 台计算机遇到蓝屏|
|度量 ID |16507562|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同的计算机，这些计算机由于显卡驱动程序二进制文件中的崩溃而发生了蓝屏（相对于总体）   。
2. 出现蓝屏的计算机数 = 计数（使用给定驱动程序版本且出现蓝屏的计算机） 
3. 计算机总数 = 计数（使用给定版本驱动程序的计算机数） 
4. 蓝屏计算机的比率 = 出现蓝屏的计算机数/计算机总数 

### <a name="final-calculation"></a>最终计算

5. 相对于总体的蓝屏计算机命中数 = 蓝屏计算机的比率 * 10,000 
6. 结果规范化为 10,000 台计算机，最终计算为： 
    
    i. [相对于总体的蓝屏计算机命中数] 10,000 台计算机中由于显卡驱动程序二进制文件中的崩溃而发生蓝屏的不同计算机数