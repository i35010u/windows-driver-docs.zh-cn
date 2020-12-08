---
title: 将 IRP 向下传递到较低级别的驱动程序
description: 将 IRP 向下传递到较低级别的驱动程序
keywords:
- IRP 调度例程 WDK 文件系统，并将 IRP 向下传递
- 将 Irp 向下传递设备堆栈 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3578ea1cb67e9b0c6f61a78b4bf2554f81027e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816271"
---
# <a name="passing-the-irp-down-to-lower-level-drivers"></a>将 IRP 向下传递到较低级别的驱动程序


## <span id="ddk_passing_the_irp_down_to_lower_level_drivers_if"></span><span id="DDK_PASSING_THE_IRP_DOWN_TO_LOWER_LEVEL_DRIVERS_IF"></span>


默认情况下，每个调度例程在检查 IRP 的目标设备对象之后，都必须通过调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将 irp 向下传递到下一个较低级别的设备驱动程序。 尤其重要的是，筛选器驱动程序会将它无法识别的任何 Irp 传递给你，而不是仅仅对它们进行故障转移。 不熟悉的 Irp 会导致操作系统本身以意外的方式失败。 例如， \_ \_ 在文件系统筛选器驱动程序中失败的 IRP MJ PNP 请求会阻止系统休眠，从而干扰电源管理。 尽管不涉及到文件系统筛选器驱动程序，并且不会收到 [**IRP \_ MJ \_ 电源**](../kernel/irp-mj-power.md) 请求，但这一点很有意义。

 

