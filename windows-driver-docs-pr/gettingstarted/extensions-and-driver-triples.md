---
title: KMDF 扩展和三重驱动程序
description: 在本主题中，我们介绍内核模式驱动程序框架 (KMDF) 基于类的扩展。
ms.assetid: 49207485-AFDF-4E84-B39C-A14FC7E2CF60
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a08581620dad4b82d279c93e26f1ad682e227d7
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63371299"
---
# <a name="kmdf-extensions-and-driver-triples"></a>KMDF 扩展和三重驱动程序


在本主题中，我们介绍内核模式驱动程序框架 (KMDF) 基于类的扩展。 在阅读本主题之前，应了解[微型驱动程序和驱动程序对](minidrivers-and-driver-pairs.md)和[作为通用驱动程序对模型的 KMDF](kmdf-as-a-generic-pair-model.md) 中介绍的理念。

对于某些设备类，Microsoft 会提供 KMDF 扩展，这些扩展会进一步降低必须由 KMDF 驱动程序执行处理的量。 使用基于类的 KMDF 扩展的驱动程序有以下三个部分，我们将其称为“三重驱动程序”  。

-   框架，处理大部分驱动程序共同的任务
-   基于类的框架扩展，处理特定于特殊类的设备的任务
-   KMDF 驱动程序，处理特定于特殊设备的任务。

三重驱动程序（KMDF 驱动程序、设备类 KMDF 扩展、框架）中的三个驱动程序合并形成单个 WDM 驱动程序。

设备类 KMDF 扩展示例为 SpbCx.sys，它为简易外围总线 (SPB) 设备类的 KMDF 扩展。 SPB 类包含同步串行总线，如 I2C 和 SPI。 I2C 总线控制器的三重驱动程序如下所示：

-   框架处理大部分驱动程序共同的常规任务。
-   SpbCx.sys 处理特定于 SPB 总线类的任务。 以下为所有 SPB 总线共同的任务。
-   KMDF 驱动程序处理特定于 I2C 总线的任务。 我们将此驱动程序称为 MyI2CBusDriver.sys。

![KMDF 驱动程序的三重扩展](images/kmdfdrivertriple.png)

三重驱动程序中的三个驱动程序（MyI2CBusDriver.sys、SpbCx.sys、Wdf01000.sys）合并形成单个 WDM 驱动程序，该驱动程序用作 I2C 总线控制器的函数驱动程序。 Wdf01000.sys（框架）拥有此驱动程序的调度表，因此当某人将 IRP 发送至三重驱动程序时，它会转至 wdf01000.sys。 如果 wdf01000.sys 本身可以处理 IRP，则不会涉及到 SpbCx.sys 和 MyI2CBusDriver.sys。 如果 wdf01000.sys 本身无法处理 IRP，则它可以通过调用 SbpCx.sys 中的事件处理程序来获取帮助。

以下是可以由 MyI2CBusDriver.sys 实现的事件处理程序的一些示例：

-   EvtSpbControllerLock
-   EvtSpbIoRead
-   EvtSpbIoSequence

以下是可以由 SpbCx.sys 实现的事件处理程序的一些示例

-   EvtIoRead

 

 





