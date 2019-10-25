---
title: SD 总线驱动程序设计指南
description: SD 总线驱动程序设计指南
ms.assetid: c082d86c-8f81-41ef-afac-bd9fd76696fd
keywords:
- SD WDK 总线
- 总线 WDK, SD
- 安全数字 WDK 总线
- 内存卡 WDK SD 总线
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: 52b8d72daa37b4e369da27c63f61552dea54569c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824741"
---
# <a name="sd-bus-driver-design-guide"></a>SD 总线驱动程序设计指南

[SD Card Driver Stack](https://docs.microsoft.com/windows-hardware/drivers/sd/sd-card-driver-stack)（SD 卡驱动程序堆栈）

[Opening, Initializing and Closing an SD Card Bus Interface](https://docs.microsoft.com/windows-hardware/drivers/sd/opening--initializing-and-closing-an-sd-card-bus-interface)（打开、初始化和关闭 SD 卡总线接口）

[Handling SD Card Interrupts](https://docs.microsoft.com/windows-hardware/drivers/sd/handling-sd-card-interrupts)（处理 SD 卡中断）

[SD Card Requests](https://docs.microsoft.com/windows-hardware/drivers/sd/sd-card-requests)（SD 卡请求）

## <a name="sd-card-hardware-identifiers"></a>SD 卡硬件标识符

有关安全数字 (SD) 设备标识字符串的信息，请参阅 [Identifiers for Secure Digital (SD) Devices](https://docs.microsoft.com/windows-hardware/drivers/install/identifiers-for-secure-digital--sd--devices)（安全数字 (SD) 设备的标识符）。

## <a name="restrictions-on-sd-card-drivers"></a>SD 卡驱动程序的限制

某些限制适用于安全数字 (SD) 卡设备驱动程序，这些驱动程序管理 SD 组合或多功能卡上的功能。 多功能卡上的各种卡功能的驱动程序堆栈必须互相独立地运行。 为了确保这种独立性，总线驱动程序会拒绝以下操作：

- 用于更改设备状态的 SD 命令，例如 SELECT\_CARD。

- SD I/O 命令，这些命令指定函数 0 但超出函数基本寄存器 (FBR) 中指定的地址范围。

- SD I/O 命令，这些命令指定另一设备堆栈的函数编号。

SD 设备驱动程序可以管理主控制器的常用寄存器集和设备的状态，只需使用类型为 SDRF\_GET\_PROPERTY 和 SDRF\_SET\_PROPERTY 的函数请求调用 [**SdBusSubmitRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequest) 即可。 如需这些函数请求类型的说明，请参阅 [**SD\_REQUEST\_FUNCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sd_request_function)。

## <a name="sd-bus-sample"></a>SD 总线示例

这是功能性安全数字 (SD) IO 驱动程序的一个示例。 该驱动程序使用内核模式驱动程序框架编写。 它是一个用于常规 mars 开发板的驱动程序，可实现 SDIO 协议而不需其他功能。

从 GitHub 下载[存储 SDIO 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617953)。
