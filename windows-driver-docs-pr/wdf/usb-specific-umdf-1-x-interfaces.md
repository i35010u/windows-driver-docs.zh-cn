---
title: 特定于 USB 的 UMDF 1.x 接口
description: 特定于 USB 的 UMDF 1.x 接口
ms.assetid: b458d96d-e15e-4a9b-a26e-490620cec38e
keywords:
- UMDF WDK，UMDF USB 对象模型
- 用户模式驱动程序框架 WDK，UMDF USB 对象模型
- 用户模式驱动程序 WDK UMDF，UMDF USB 对象模型
- UMDF USB 对象模型 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 702f67395737f4897e5f68cd28f56fd70dd1f45c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376671"
---
# <a name="usb-specific-umdf-1x-interfaces"></a>特定于 USB 的 UMDF 1.x 接口


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

USB 设备可具有一个或多个配置。 每个配置可以有一个或多个接口。 每个接口相关联与一个或多个备用的设置，并且每个备用设置定义一个或多个终结点。 终结点表示设备硬件上的缓冲区。

管道是连接的一种软件抽象的主控制器和当前的备用设置中的终结点之间。 管道可以是针对 I/O，并通过 UMDF 中公开[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)接口。

特定于 USB 的 UMDF 接口构建的[WinUSB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)体系结构。 根据设计，WinUSB 只允许访问多个配置设备的第一个配置。 因此，WinUSB 接口不会显示将提交一个选择配置请求的功能。 因此，在 UMDF 的 I/O 目标功能不支持选择第一个以外的任何设备配置。

特定于 USB 的 UMDF 接口具有类似于常规的 USB 模型的对象层次结构。 UMDF 驱动程序创建一个目标设备对象，它通过公开[IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)接口。 该驱动程序然后可以使用 IWDFUsbTargetDevice 方法来访问 USB 接口，由的实例公开[IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)。 该驱动程序可以调用 IWDFUsbInterface 方法操作设置和终结点。

下表显示了特定于 USB 的 UMDF 界面层次结构：

| 特定于 USB 的 UMDF 接口                    | 派生自                     |
|------------------------------------------------|----------------------------------|
| [IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice) | [IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget) |
| [IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)       | [IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject)     |
| [IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)     | [IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget) |

 

[IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)并[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)接口派生自[IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget)接口，并因此，公开 I/O 目标对象。 [IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)接口不是派生 IWDFIoTarget (派生自 IWDFUsbInterface [IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject)接口)，因此，不显示 I/O 目标对象。 任何发送，以发现和操作接口的详细信息的 I/O 发送到目标设备。

有关编写简单的基于 UMDF 的 USB 客户端驱动程序的分步说明，请参阅[如何编写第一个 USB 客户端驱动程序 (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

若要了解有关所需的 UMDF 基于 USB 客户端驱动程序的源代码，请参阅[了解 USB 客户端驱动程序代码结构 (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

 

 





