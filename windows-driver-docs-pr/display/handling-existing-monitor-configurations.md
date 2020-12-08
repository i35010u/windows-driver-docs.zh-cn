---
title: 处理现有的监视器配置
description: 处理现有的监视器配置
keywords:
- 监视配置 WDK 显示，还原上一项
- 监视配置 WDK 显示，现有监视器
- TMM WDK 显示，现有监视器配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ad6fd89b2285e92ffabbdc758ddae07dcde0d6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819115"
---
# <a name="handling-existing-monitor-configurations"></a>处理现有的监视器配置


除了在双监视器配置中检测新的监视器和启动 TMM 对话框之外，TMM 还必须还原以前的显示配置。 TMM 可以通过 [**IViewHelper：： SetConfiguration**](/previous-versions/windows/hardware/drivers/ff568176(v=vs.85)) 方法将显示数据传递到用户模式显示驱动程序来还原显示配置。 TMM 将分配内存并将显示模式和拓扑信息存储在内存中。 TMM 将此内存传递到 **SetConfiguration** 的 *pIStream* 参数指向的 **IStream** 接口。 用户模式显示驱动程序还可以修改或折叠其他显示数据 (例如，伽玛或电视设置) 。 当驱动程序完成显示数据后，驱动程序将调用 **IStream：： Release** 方法来释放内存。

下图显示了在 TMM 还原现有的监视器配置时所发生的操作流。

![说明如何还原现有监视器配置的关系图](images/tmm-existconfig.png)

 

