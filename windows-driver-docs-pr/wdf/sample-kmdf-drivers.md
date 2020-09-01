---
title: 示例 KMDF 驱动程序
description: 本主题列出了可从 Windows 开发人员中心-硬件下载的 (KMDF) 示例驱动程序的内核模式驱动程序框架。
ms.assetid: 83d15b96-63b1-4584-8ef4-ccbdcc1522bb
keywords:
- 内核模式驱动程序 WDK KMDF，示例
- KMDF WDK，示例驱动程序
- 内核模式驱动程序框架 WDK，示例驱动程序
- 基于框架的驱动程序 WDK KMDF，示例
- 示例驱动程序 WDK KMDF
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: d318168d52eb94943dc7f3096098eaa97045c790
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189637"
---
# <a name="sample-kmdf-drivers"></a>示例 KMDF 驱动程序

本主题列出了可以在 [Microsoft 示例门户](/samples/browse/?products=windows-wdk)上浏览和下载 (KMDF) 示例驱动程序的内核模式驱动程序框架。 还可以在 GitHub 上克隆、分叉或下载 [Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) 存储库。

有关生成这些示例的信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

<a href="" id="echo"></a>ECHO 演示了如何使用框架的队列并请求对象和自动同步。

有关此示例的详细信息，请参阅 [KMDF Echo 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf)。

<a href="" id="fakemodem"></a>FakeModem 演示了一个简单的 controllerless 调制解调器驱动程序，该驱动程序发送和接收命令。

有关此示例的详细信息，请参阅 [Fakemodem 驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/modem/fakemodem)。

<a href="" id="firefly"></a>FIREFLY 演示了如何使用 i/o 控制代码 (IOCTLs) 在 (HID) 设备上编程人工输入设备，并提供 Windows Management Instrumentation (WMI) 接口。

有关此示例的详细信息，请参阅 [FIREFLY](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)。

<a href="" id="hidusbfx2"></a>HIDUSBFX2 演示如何编写 HID 设备的微型驱动程序，以及如何将非 HID USB 设备映射到 HID 设备。 设备包含在 OSR USB-FX2 Learning 工具包中。

有关此示例的详细信息，请参阅 [HIDUSBFX2](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/hidusbfx2)。

<a href="" id="kbfiltr"></a>KbFiltr 演示 PS/2 键盘的上层设备筛选器驱动程序。

有关此示例的详细信息，请参阅 [键盘输入 WDF 筛选器驱动程序 (Kbfiltr) ](https://github.com/Microsoft/Windows-driver-samples/tree/master/input/kbfiltr)。

<a href="" id="ndisprot"></a>NDISProt 演示了连接性更少的 NDIS 5.0/5.1 和 NDIS 6.0 协议驱动程序。

有关此示例的详细信息，请参阅 [NDISProt 无连接的 WDF 协议](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/ndisprot_kmdf)。

<a href="" id="nonpnp"></a>NONPNP 演示了使用框架的非即插即用 (PnP) 驱动程序。

有关此示例的详细信息，请参阅 [NONPNP](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl/kmdf)。

<a href="" id="kmdf-fx2"></a>KMDF \_ FX2 演示了如何对 OSR USB FX2 学习工具包中包含的 usb 设备执行批量和中断数据传输。

有关此示例的详细信息，请参阅 [kmdf \_ fx2](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/kmdf_fx2)。

<a href="" id="pcidrv"></a>PCIDRV 10/100) 和 Intel 兼容机，为基于 Intel 82557/82558 的 PCI 以太网 (适配器提供功能齐全的基于框架的驱动程序。

有关此示例的详细信息，请参阅适用于 [PCI 设备的 PCIDRV 驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/pcidrv)。

<a href="" id="plx9x5x"></a>PLX9x5x 演示如何为支持 DMA 的通用 PCI 设备编写驱动程序并使用 PLX9656/9653RDK。

有关此示例的详细信息，请参阅 [PLX9X5X PCI 驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/PLX9x5x)。

<a href="" id="serial"></a>针对基于该 WDM 串行示例驱动程序的基于框架的串行驱动程序进行串行。

有关此示例的详细信息，请参阅 [序列示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)。

<a href="" id="toaster"></a>Toaster 基于框架的 WDM Toaster 示例驱动程序版本。 Toaster 示例包含一个筛选器驱动程序、一个函数驱动程序和一个用于创建单个驱动程序堆栈的总线驱动程序。 该示例还包括一个额外的内核模式驱动程序，该驱动程序使用远程 i/o 目标与驱动程序堆栈进行通信。

有关此示例的详细信息，请参阅 [Toaster](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv)。

<a href="" id="usbsamp"></a>UsbSamp 演示如何使用框架执行到 USB 设备的大容量和同步数据传输。

有关此示例的详细信息，请参阅 [Usbsamp 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/usbsamp)。

<a href="" id="wmisamp"></a>WmiSamp 演示了如何为框架设备对象注册 WMI 提供程序和创建提供程序实例，以及如何处理应用程序发送到设备的 WMI 查询。

有关此示例的详细信息，请参阅 [WMISAMP WMI 提供程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/wmi/wmisamp)。