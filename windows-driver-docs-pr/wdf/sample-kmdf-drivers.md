---
title: 示例 KMDF 驱动程序
description: 本主题列出了你可以从 Windows 开发人员中心-硬件下载的内核模式驱动程序框架 (KMDF) 示例驱动程序。
ms.assetid: 83d15b96-63b1-4584-8ef4-ccbdcc1522bb
keywords:
- 内核模式驱动程序 WDK KMDF，示例
- KMDF WDK，示例驱动程序
- 内核模式驱动程序框架 WDK 示例驱动程序
- 基于框架的驱动程序 WDK KMDF，示例
- 示例驱动程序 WDK KMDF
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae5b17e143aa3db86f410df40c130337065ff8bc
ms.sourcegitcommit: 2589492f3c14f779efa8b446e81d4e0f6d048f4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815090"
---
# <a name="sample-kmdf-drivers"></a>示例 KMDF 驱动程序


本主题列出了您可以从下载的内核模式驱动程序框架 (KMDF) 示例驱动程序[Windows 驱动程序示例存储库](https://github.com/Microsoft/Windows-driver-samples)GitHub 上。




生成示例的信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

<a href="" id="echo"></a>ECHO 演示如何使用 framework 的队列和请求对象，并自动同步。

有关此示例的详细信息，请参阅[KMDF Echo 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf)。

<a href="" id="fakemodem"></a>FakeModem 演示一个简单的 controllerless 调制解调器驱动程序发送和接收 AT 命令。

有关此示例的详细信息，请参阅[Fakemodem 驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/modem/fakemodem)。

<a href="" id="firefly"></a>FIREFLY 演示编程人工输入设备 (HID) 设备使用 I/O 控制代码 (Ioctl)，并提供 Windows Management Instrumentation (WMI) 接口。

有关此示例的详细信息，请参阅[萤火虫的 HID 设备的 WDF 筛选器驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)。

<a href="" id="hidusbfx2"></a>HIDUSBFX2 演示如何编写 HID 设备的微型驱动程序以及如何映射到 HID 设备的非-HID USB 设备。 设备包含在 OSR USB FX2 学习工具包。

有关此示例的详细信息，请参阅[HIDUSBFX2](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/hidusbfx2)。

<a href="" id="kbfiltr"></a>KbFiltr 演示 ps/2 键盘上的设备筛选器驱动程序。

有关此示例的详细信息，请参阅[键盘输入 WDF 筛选器驱动程序 (Kbfiltr)](https://github.com/Microsoft/Windows-driver-samples/tree/master/input/kbfiltr)。

<a href="" id="ndisprot"></a>NDISProt 演示的无连接的 NDIS 5.0/5.1 和 NDIS 6.0 协议驱动程序。

有关此示例的详细信息，请参阅[NDISProt 无连接的 WDF 协议](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/ndisprot_kmdf)。

<a href="" id="nonpnp"></a>NONPNP 演示使用框架的非即插 (PnP) 驱动程序。

有关此示例的详细信息，请参阅[NONPNP](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl/kmdf)。

<a href="" id="kmdf-fx2"></a>KMDF\_FX2 演示如何执行大容量和中断数据传输到 OSR USB FX2 学习工具包中包含的 USB 设备。

有关此示例的详细信息，请参阅[kmdf\_fx2](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/kmdf_fx2)。

<a href="" id="pcidrv"></a>PCIDRV 一个完全正常运行基于 framework 的驱动程序的基于 Intel 82557/82558 PCI 以太网适配器 (10/100) 和 Intel 兼容对象。

有关此示例的详细信息，请参阅[PCIDRV-PCI 设备 WDF 驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/pcidrv)。

<a href="" id="plx9x5x"></a>PLX9x5x 演示如何编写支持 DMA，并使用 PLX9656/9653RDK LITE 板的通用 PCI 设备的驱动程序。

有关此示例的详细信息，请参阅[PLX9x5x PCI 驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/PLX9x5x)。

<a href="" id="serial"></a>串行的基于框架的串行驱动程序基于 WDM 串行示例驱动程序。

有关此示例的详细信息，请参阅[串行示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)。

<a href="" id="toaster"></a>Toaster 基于 Framework 的版本的 WDM toaster 示例驱动程序。 Toaster 示例包括筛选器驱动程序、 功能驱动程序，并创建一个驱动程序堆栈的总线驱动程序。 此示例还包含用于远程 I/O 目标通信与驱动程序堆栈的其他内核模式驱动程序。

有关此示例的详细信息，请参阅[Toaster](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv)。

<a href="" id="usbsamp"></a>UsbSamp 演示如何使用该框架来执行大容量和同步数据传输到 USB 设备。

有关此示例的详细信息，请参阅[Usbsamp 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/usbsamp)。

<a href="" id="wmisamp"></a>WmiSamp 演示如何以注册 WMI 提供程序并创建设备对象的框架的提供程序实例以及如何处理应用程序发送到设备的 WMI 查询。

有关此示例的详细信息，请参阅[WmiSamp WMI 提供程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/wmi/wmisamp)。


