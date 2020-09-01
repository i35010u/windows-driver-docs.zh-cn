---
title: 处理现有的监视器配置
description: 处理现有的监视器配置
ms.assetid: b2da12ea-cbcd-4754-a65f-e54ed305f5d7
keywords:
- 监视配置 WDK 显示，还原上一项
- 监视配置 WDK 显示，现有监视器
- TMM WDK 显示，现有监视器配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d50a14d6693dd5568465337b131cc4140ee4b42c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064802"
---
# <a name="handling-existing-monitor-configurations"></a>处理现有的监视器配置


除了在双监视器配置中检测新的监视器和启动 TMM 对话框之外，TMM 还必须还原以前的显示配置。 TMM 可以通过 [**IViewHelper：： SetConfiguration**](/previous-versions/windows/hardware/drivers/ff568176(v=vs.85)) 方法将显示数据传递到用户模式显示驱动程序来还原显示配置。 TMM 将分配内存并将显示模式和拓扑信息存储在内存中。 TMM 将此内存传递到**SetConfiguration**的*pIStream*参数指向的**IStream**接口。 用户模式显示驱动程序还可以修改或折叠其他显示数据 (例如，伽玛或电视设置) 。 当驱动程序完成显示数据后，驱动程序将调用 **IStream：： Release** 方法来释放内存。

下图显示了在 TMM 还原现有的监视器配置时所发生的操作流。

![说明如何还原现有监视器配置的关系图](images/tmm-existconfig.png)

 

