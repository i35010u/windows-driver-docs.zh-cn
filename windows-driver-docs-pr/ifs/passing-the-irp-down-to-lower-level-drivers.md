---
title: 将 IRP 向下传递到较低级别的驱动程序
description: 将 IRP 向下传递到较低级别的驱动程序
ms.assetid: 9a8e72fb-b0a8-4026-8606-57fa03344146
keywords:
- IRP 调度例程 WDK 文件系统，并将 IRP 向下传递
- 将 Irp 向下传递设备堆栈 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a78b3a0a11f554e1fd77c94992e438ffa20a73da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841043"
---
# <a name="passing-the-irp-down-to-lower-level-drivers"></a>将 IRP 向下传递到较低级别的驱动程序


## <span id="ddk_passing_the_irp_down_to_lower_level_drivers_if"></span><span id="DDK_PASSING_THE_IRP_DOWN_TO_LOWER_LEVEL_DRIVERS_IF"></span>


默认情况下，每个调度例程在检查 IRP 的目标设备对象之后，都必须通过调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将 irp 向下传递到下一个较低级别的设备驱动程序。 尤其重要的是，筛选器驱动程序会将它无法识别的任何 Irp 传递给你，而不是仅仅对它们进行故障转移。 不熟悉的 Irp 会导致操作系统本身以意外的方式失败。 例如，失败的 IRP\_MJ\_文件系统筛选器驱动程序中的 PNP 请求会阻止系统休眠，从而干扰电源管理。 尽管不会将文件系统筛选器驱动程序包括在电源管理中，也不会接收[**IRP\_MJ\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) requests，

 

 




