---
title: 处理现有的监视器配置
description: 处理现有的监视器配置
ms.assetid: b2da12ea-cbcd-4754-a65f-e54ed305f5d7
keywords:
- 监视配置 WDK 显示，请还原上一个
- 监视器配置 WDK 显示现有监视器
- TMM WDK 显示，现有监视器配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 322bd3a7737266c46224238be5b48ca34f8869d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382317"
---
# <a name="handling-existing-monitor-configurations"></a>处理现有的监视器配置


除了检测新的监视器和启动 TMM 对话框中的两个监视器配置，TMM 还必须还原以前显示的配置。 TMM 可以通过将显示数据传递给用户模式显示驱动程序通过还原显示配置[ **IViewHelper::SetConfiguration** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568176(v=vs.85))方法。 TMM 将分配的内存和存储在内存中的显示模式和拓扑信息。 TMM 将传递在此内存**IStream**界面*pIStream*参数**SetConfiguration**指向。 用户模式显示驱动程序还可以修改或折叠其他显示数据 （例如，gamma 或电视设置） 中。 当驱动程序完成了显示数据时，该驱动程序调用**IStream::Release**方法来释放内存。

下图显示了发生 TMM 还原现有的监视配置时的操作的流。

![说明还原现有的监视配置的关系图](images/tmm-existconfig.png)

 

 





