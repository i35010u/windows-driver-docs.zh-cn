---
title: 智能卡驱动程序环境
description: 智能卡驱动程序环境
ms.assetid: f1b369c6-84a0-4a0a-9e70-40dd3009c59e
keywords:
- 智能卡驱动程序 WDK、 环境
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92cc9c9d2fe9b901576b86705ece238aed27c7f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379775"
---
# <a name="smart-card-driver-environment"></a>智能卡驱动程序环境


## <span id="_ntovr_smart_card_driver_environment"></span><span id="_NTOVR_SMART_CARD_DRIVER_ENVIRONMENT"></span>


下图显示了智能卡读卡器驱动程序的标准环境。

![说明用于智能卡读卡器驱动程序的标准环境的关系图](images/memp1.png)

此外，该图显示了智能卡环境的以下组件：

-   应用程序通过智能卡资源管理器与智能卡读卡器驱动程序进行通信。 读卡器驱动程序位于内核空间，并且智能卡资源管理器驻留在用户空间中。

-   使用调度的 I/O 控制通过资源管理器与读卡器驱动程序进行通信[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=94613)系统调用。 有关如何使用信息[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=94613)系统调用，请参阅[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=94613) Microsoft Windows SDK 中的主题。

    同样，可识别智能卡的应用程序可以将指令发送到通过智能卡读卡器驱动程序[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=94613)，，操作系统将转发到读卡器驱动程序所指示的 IOCTL。 如果读卡器驱动程序是一个 WDM 驱动程序，操作系统将请求转发到 I/O 请求数据包 (IRP) 通过。

-   Microsoft 提供了一个读取器驱动程序示例*pscr.sys*，这是用于 PCMCIA 智能卡读卡器的驱动程序。 此驱动程序的源代码是 WDK 示例集合中可用。 有关详细信息，请参阅[PCMCIA 智能卡驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/smartcrd)。 智能卡读取器设备的供应商必须提供用于处理系统提供的资源管理器和智能卡驱动程序库的驱动程序。

-   这两个本机和供应商提供的读卡器驱动程序必须使用智能卡驱动程序库来执行其密钥的操作的许多节中所述[智能卡驱动程序库](smart-card-driver-library.md)。

 

 





