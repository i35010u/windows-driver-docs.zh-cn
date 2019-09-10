---
title: 至少有一次音频流初始化失败的计算机的百分比
description: 该度量将 7 天滑动窗口中的遥测数据聚合为至少有一次意外的初始化失败的计算机所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 0f90e511c755ff8e9b8bfefd641adeb982b85496
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223941"
---
# <a name="percent-of-machines-with-at-least-one-audio-stream-initialization-failure"></a>至少有一次音频流初始化失败的计算机的百分比

## <a name="description"></a>描述

如果设备无法初始化音频流，用户将无法访问应用程序的音频体验。 此度量计算具有无法初始化流的音频设备的计算机所占的百分比。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天滑动窗口|
|度量标准 |计算机的聚合|
|最小总体数量 |50 台计算机|
|通过标准 |<= 8% 的计算机至少有 1 次音频流初始化失败|
|度量 ID |12111510|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为至少有一次意外的初始化失败的计算机所占的百分比 
2. 发生初始化失败的计算机数 = 计数（至少有 1 次意外的初始化失败的计算机数） 
3. 计算机总数 = 计数（尝试初始化音频流的计算机数） 

### <a name="final-calculation"></a>最终计算

至少有 1 次流初始化失败的计算机的百分比 = 发生初始化失败的计算机数/计算机总数 
