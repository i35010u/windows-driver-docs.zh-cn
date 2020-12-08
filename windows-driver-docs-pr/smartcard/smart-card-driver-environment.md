---
title: 智能卡驱动程序环境
description: 智能卡驱动程序环境
keywords:
- 智能卡驱动程序 WDK，环境
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dace8ac4e6dff965a0851f560a4d76401197bdf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811905"
---
# <a name="smart-card-driver-environment"></a>智能卡驱动程序环境


## <span id="_ntovr_smart_card_driver_environment"></span><span id="_NTOVR_SMART_CARD_DRIVER_ENVIRONMENT"></span>


下图显示了智能卡读卡器驱动程序的标准环境。

![说明智能卡读卡器驱动程序的标准环境的示意图](images/memp1.png)

此外，该图显示了智能卡环境的下列组件：

-   应用程序通过智能卡资源管理器与智能卡读卡器驱动程序通信。 读取器驱动程序驻留在内核空间中，而智能卡资源管理器位于用户空间。

-   资源管理器通过使用 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 系统调用调度的 i/o 控件来与读取器驱动程序通信。 有关如何使用 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 系统调用的信息，请参阅 Microsoft Windows SDK 中的 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 主题。

    同样，智能卡感知应用程序可以通过 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)将指令发送到智能卡读卡器驱动程序，操作系统将指示的 IOCTL 转发到读取器驱动程序。 如果读取器驱动程序为 WDM 驱动程序，操作系统将通过 i/o 请求数据包转发请求 (IRP) 。

-   Microsoft 提供一个读卡器驱动程序示例， *pscr.sys*，这是一个 PCMCIA 智能卡读卡器的驱动程序。 该驱动程序的源代码在 WDK 示例的集合中提供。 有关详细信息，请参阅 [PCMCIA 智能卡驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/smartcrd)。 智能卡读卡器设备的供应商必须提供旨在使用系统提供的资源管理器和智能卡驱动程序库的驱动程序。

-   本机和供应商提供的读取器驱动程序都必须使用智能卡驱动程序库来执行其许多关键操作，如 " [智能卡驱动程序库](smart-card-driver-library.md)" 一节中所述。

 

