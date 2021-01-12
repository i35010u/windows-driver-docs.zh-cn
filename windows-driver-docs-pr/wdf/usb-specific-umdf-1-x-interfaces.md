---
title: 特定于 USB 的 UMDF 1.x 接口
description: 特定于 USB 的 UMDF 1.x 接口
keywords:
- UMDF WDK，UMDF-USB 对象模型
- User-Mode Driver Framework WDK，UMDF-USB 对象模型
- 用户模式驱动程序 WDK UMDF，UMDF-USB 对象模型
- UMDF-USB 对象模型 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 280b224e4827b7f301e74d513d99265be0e17d4d
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124109"
---
# <a name="usb-specific-umdf-1x-interfaces"></a>特定于 USB 的 UMDF 1.x 接口


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

USB 设备可以有一个或多个配置。 每个配置可以有一个或多个接口。 每个接口都与一个或多个备用设置相关联，并且每个替代设置定义一个或多个终结点。 终结点表示设备硬件上的缓冲区。

管道是主机控制器与当前替代设置中的终结点之间的连接的软件抽象。 管道可以是 i/o 的目标，并通过 [IWDFUsbTargetPipe](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe) 接口在 UMDF 中公开。

在 [WinUSB](../usbcon/winusb.md) 体系结构的基础上构建 USB 特定的 UMDF 接口。 按照设计，WinUSB 只允许访问多个配置设备的第一个配置。 因此，WinUSB 接口不会公开提交选择配置请求的功能。 因此，UMDF 中的 i/o 目标功能不支持选择除第一个以外的任何设备配置。

USB 特定的 UMDF 接口具有与常规 USB 模型类似的对象层次结构。 UMDF 驱动程序创建一个由 [IWDFUsbTargetDevice](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) 接口公开的目标设备对象。 然后，该驱动程序可以使用 IWDFUsbTargetDevice 的方法来访问 USB 接口，这些接口由 [IWDFUsbInterface](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)的实例公开。 驱动程序可以调用 IWDFUsbInterface 方法来处理设置和终结点。

下表显示了 USB 特定的 UMDF 接口层次结构：

| USB 特定的 UMDF 接口                    | 派生                     |
|------------------------------------------------|----------------------------------|
| [IWDFUsbTargetDevice](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) | [IWDFIoTarget](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget) |
| [IWDFUsbInterface](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)       | [IWDFObject](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)     |
| [IWDFUsbTargetPipe](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)     | [IWDFIoTarget](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget) |

 

[IWDFUsbTargetDevice](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)和[IWDFUsbTargetPipe](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)接口派生自[IWDFIoTarget](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)接口，因此，公开 i/o 目标对象。 [IWDFUsbInterface](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)接口不派生自 IWDFIoTarget (IWDFUsbInterface 派生自[IWDFObject](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)接口) ，因此不公开 i/o 目标对象。 发送到发现和操作接口详细信息的任何 i/o 都将发送到目标设备。

有关编写简单的基于 UMDF 的 USB 客户端驱动程序的分步说明，请参阅 [如何编写第一个 USB 客户端驱动程序 (UMDF) ](/windows-hardware/drivers/ddi/index)。

若要了解基于 UMDF 的 USB 客户端驱动程序所需的源代码，请参阅 [了解 usb 客户端驱动程序代码结构 (umdf) ](/windows-hardware/drivers/ddi/index)。

