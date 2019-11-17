---
title: 超出了 ESRT 的固件最大重试限制的计算机百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为达到最大重试限制的计算机数与出现安装事件的计算机数的比率
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 68e996c34dc638c43955a3e2ef05b97d67e9cb92
ms.sourcegitcommit: 07b2926c15f4782e1914e8d3cf6c5c511a3a6111
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2019
ms.locfileid: "74097489"
---
# <a name="percent-of-machines-exceeded-firmware-max-retry-limit-from-esrt"></a>超出了 ESRT 的固件最大重试限制的计算机百分比

## <a name="description"></a>描述

尝试安装固件成功但超出固件最大重试限制（默认为 3 次）的计算机的百分比

该度量将 28 天滑动窗口中的遥测数据聚合为达到最大重试限制的计算机数与出现安装事件的计算机数的比率

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |200|
|通过标准 |<= 5%|
|度量 ID |20116755|

## <a name="calculation"></a>计算

安装了固件但达到最大重试限制的计算机数/

收到了固件设备的驱动程序安装事件的计算机数

