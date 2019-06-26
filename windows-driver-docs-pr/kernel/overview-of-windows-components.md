---
title: Windows 组件概述
description: Windows 组件概述
ms.assetid: b941197d-732c-4b9a-8367-46beb14c33cf
keywords:
- Windows 组件 WDK
- Windows NT 组件 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44537db010e89498573f4ec73b061fe0e40a4efb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383816"
---
# <a name="overview-of-windows-components"></a>Windows 组件概述





下图显示了 Windows 操作系统的主要内部组件。

![说明 windows 组件的概述关系图](images/ntarch.png)

如图所示，Windows 操作系统包括用户模式和内核模式组件。 有关 Windows 用户和内核模式的详细信息，请参阅[用户模式和内核模式](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode)。

驱动程序调用由各种内核组件导出的例程。 例如，若要创建一个设备对象，将调用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice) I/O 管理器导出的例程。 内核模式驱动程序可以调用的例程的列表，请参阅[驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

此外，驱动程序必须响应来自操作系统的特定的调用，并能够响应其他系统调用。 有关驱动程序可能需要支持的内核模式例程的列表，请参阅[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)。

并非所有内核模式组件是在上图中所都示。 内核模式组件的列表，请参阅[内核模式下管理器和库](kernel-mode-managers-and-libraries.md)。

 

 




