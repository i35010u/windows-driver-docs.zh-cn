---
title: 在过去 28 天内 WU 报告成功下载的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为已报告从 Windows 更新成功进行了下载的计算机数的比率
ms.topic: article
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: ee75ce1be42905004068ced6bfefedea6967a1e5
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "79083189"
---
# <a name="percent-of-machines-that-wu-reported-a-successful-download-within-the-last-28-days"></a>在过去 28 天内 WU 报告成功下载的计算机的百分比

## <a name="description"></a>说明

在过去 28 天内 WU 报告成功下载的计算机的百分比

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |100|
|通过标准 |>= 95%|
|度量 ID |24186432|

## <a name="calculation"></a>计算

WU 报告成功下载 (status == 0) 的计算机数/ 

已尝试 WU 下载的计算机数
