---
title: 在过去 28 天内 WU 报告成功安装的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为已报告从 Windows 更新成功进行了安装的计算机数的比率
ms.topic: article
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1bfe9a06d3d90ee124cadc9c8cfa252ea8557352
ms.sourcegitcommit: 774d42aa3392ae88f4890d901dbd3e8945cb2658
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82138638"
---
# <a name="percent-of-machines-that-wu-reported-a-successful-installation-within-the-last-28-days"></a>在过去 28 天内 WU 报告成功安装的计算机的百分比

## <a name="description"></a>说明

在过去 28 天内 WU 报告成功安装的计算机的百分比 

有关“Windows 更新”错误代码的详细信息，请参阅：
* [按组件列出的“Windows 更新”错误代码](https://docs.microsoft.com/windows/deployment/update/windows-update-error-reference)
* [“Windows 更新”常见错误和缓解措施](https://docs.microsoft.com/windows/deployment/update/windows-update-errors)

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |100|
|通过标准 |>= 95%|
|度量 ID |24185194|

## <a name="calculation"></a>计算

WU 报告成功安装 (status == 0) 的计算机数/ 

已尝试 WU 安装的计算机数
