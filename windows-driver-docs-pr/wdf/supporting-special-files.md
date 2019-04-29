---
title: 支持特殊文件
description: 支持特殊文件
ms.assetid: 350e715f-be36-4999-99a2-6175d9763b3f
keywords:
- 特殊文件 WDK KMDF
- 分页文件 WDK KMDF
- 转储文件 WDK KMDF
- 休眠文件 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 960698fdcd12875c75a21f7f1490401c6319cd7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385062"
---
# <a name="supporting-special-files"></a>支持特殊文件


*特殊文件*包括分页文件、 转储文件和休眠文件。 如果您的驱动程序的目标设备，则系统可能会使用这些文件的存储设备驱动程序必须执行以下操作：

-   调用[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)启用或禁用对每种类型的特殊文件的支持。 （每个驱动程序支持特殊文件禁用默认情况下。）

    总线驱动程序的[枚举子设备](enumerating-the-devices-on-a-bus.md)还应调用[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)每个子设备可以支持特殊文件。

-   调用[ **WdfDeviceAddDependentUsageDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff545864)、 支持特殊文件时，如果一台设备依赖于另一台设备。

-   （可选） 提供[ *EvtDeviceUsageNotification* ](https://msdn.microsoft.com/library/windows/hardware/ff540915) （从 KMDF 1.11） 或[ *EvtDeviceUsageNotificationEx* ](https://msdn.microsoft.com/library/windows/hardware/hh406365)回调函数，以便创建或删除特殊文件时，将通知该驱动程序。

如果您的驱动程序调用[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)对于设备，并且如果在设备上打开的特殊文件，该框架不允许即插即用管理器中删除或停用设备。

驱动程序已调用后[ **WdfDeviceAddDependentUsageDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff545864)，它可以调用[ **WdfDeviceRemoveDependentUsageDeviceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff546829)若要删除对另一台设备的设备的依赖关系。

 

 





