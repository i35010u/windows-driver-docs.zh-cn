---
title: 将 IRP 向下传递到较低级别的驱动程序
description: 将 IRP 向下传递到较低级别的驱动程序
ms.assetid: 9a8e72fb-b0a8-4026-8606-57fa03344146
keywords:
- IRP 调度例程 WDK 文件系统中，向下传递 IRP
- 将 Irp 传递下设备堆栈 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6200c24666752c8ce20eda6e72cdfa407571b558
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352779"
---
# <a name="passing-the-irp-down-to-lower-level-drivers"></a>将 IRP 向下传递到较低级别的驱动程序


## <span id="ddk_passing_the_irp_down_to_lower_level_drivers_if"></span><span id="DDK_PASSING_THE_IRP_DOWN_TO_LOWER_LEVEL_DRIVERS_IF"></span>


默认情况下每个调度例程之后检查 IRP 的目标设备对象，, 必须传递到下一个较低级别的设备驱动程序 IRP 通过调用[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。 尤其重要，筛选器驱动程序将关闭它而不是只需将其故障无法识别任何 Irp 传递给它。 失败不熟悉 Irp，可能会导致操作系统本身意想不到的方式失败。 例如，失败的 IRP\_MJ\_PNP 中的文件系统筛选器驱动程序的请求可能会干扰通过防止系统休眠电源管理。 这是 true 的情况，文件系统筛选器驱动程序不涉及中电源管理，并且不会收到[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)请求。

 

 




