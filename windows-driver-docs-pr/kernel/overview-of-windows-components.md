---
title: Windows 组件概述
description: Windows 组件概述
ms.assetid: b941197d-732c-4b9a-8367-46beb14c33cf
keywords:
- Windows 组件 WDK
- Windows NT 组件 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 0c295794930137c214ade9871d61781c197fedfa
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007629"
---
# <a name="overview-of-windows-components"></a>Windows 组件概述





下图显示了 Windows 操作系统的主要内部组件。

![阐释 windows 组件概述的关系图](images/ntarch.png)

如图所示，Windows 操作系统同时包含用户模式和内核模式组件。 有关 Windows 用户和内核模式的详细信息，请参阅[用户模式和内核模式](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode)。

驱动程序调用由各种内核组件导出的例程。 例如，若要创建设备对象，需调用由 i/o 管理器导出的[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)例程。 有关驱动程序可调用的内核模式例程的列表，请参阅[驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

此外，驱动程序必须对来自操作系统的特定调用做出响应，并可响应其他系统调用。 有关驱动程序可能需要支持的内核模式例程的列表，请参阅[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)。

并非所有内核模式组件都在上图中进行了图示。 有关内核模式组件的列表，请参阅[内核模式管理器和库](kernel-mode-managers-and-libraries.md)。

 

 




