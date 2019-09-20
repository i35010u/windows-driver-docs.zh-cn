---
title: 驱动程序安装过程成功完成的计算机的百分比
description: 该度量将 30 天滑动窗口中的遥测数据聚合为成功安装驱动程序的计算机所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: e8ad66bde87ea9efd250eb622c9fc932fcc8f427
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017023"
---
# <a name="percent-of-machines-where-the-driver-install-process-completes-successfully"></a>驱动程序安装过程成功完成的计算机的百分比

## <a name="description"></a>描述

当未能正确安装驱动程序时，目标组件会失去功能并阻止用户访问组件功能。 用户必须解决该问题以重新获取功能。 PNP 错误代码列表位于[设备管理器问题代码](https://docs.microsoft.com/windows-hardware/drivers/debugger/device-manager-problem-codes)和 [Windows 支持](https://support.microsoft.com/help/310123/error-codes-in-device-manager-in-windows)。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |展开|
|时间段 |30 天滑动窗口|
|度量标准 |计算机的聚合|
|最小总体数量 |100 台计算机|
|通过标准 |>= 95% 的计算机已成功安装驱动程序|
|度量 ID |10042840|

## <a name="calculation"></a>计算

1. 该度量将 30 天滑动窗口中的遥测数据聚合为成功安装驱动程序的计算机所占的百分比  。
2. 成功安装数 = 计数（包含成功 PNP 事件的计算机数） 
3. 总安装数 = 计数（启动驱动程序安装过程的计算机数） 

### <a name="final-calculation"></a>最终计算

PNP 成功率 = 成功安装数/总安装数 
