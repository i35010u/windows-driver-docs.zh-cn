---
title: 通用串行总线 (USB) 驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义 USB 驱动程序的起点。
ms.date: 03/24/2021
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: 19536e272b580fd7ef34d06639e59da208c340b8
ms.sourcegitcommit: 2a27786ed72024f064bbfef20933b0d0b429d4b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105106159"
---
# <a name="universal-serial-bus-usb-driver-samples"></a>通用串行总线 (USB) 驱动程序示例

USB 驱动程序示例提供了为设备编写自定义 USB 驱动程序的起点。

> [!IMPORTANT]
> 本主题适用于 USB 设备驱动程序开发人员。
>
> 如果你是遇到 USB 设备问题的 Windows 用户，请参阅 [排查常见 usb 问题](https://support.microsoft.com/help/17614/windows-10-troubleshoot-common-usb-problems)。

可以通过多种方式使用 Windows 10 USB 驱动程序示例：

- 在 [Microsoft 示例门户](/samples/browse/?products=windows-wdk)上浏览并下载单个 Windows 10 驱动程序示例。

- 在 GitHub 上克隆、分叉或下载 [Windows 驱动程序-示例](https://github.com/Microsoft/Windows-driver-samples) 存储库。

- 查看 GitHub 上的 [Windows 10 USB 驱动程序示例](https://github.com/microsoft/Windows-driver-samples/tree/master/usb) 。

可以在以下位置找到以前版本的 Windows 驱动程序示例：

- [Windows 8.1 驱动程序示例](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples)

- [Windows 8 驱动程序示例](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.0%20Samples)

- Windows [驱动程序工具包版本 7.1.0](https://www.microsoft.com/download/details.aspx?id=11800)中包含 windows 7 驱动程序示例。 驱动程序示例位于 \src 子目录 (例如，C:\WinDDK\7600.16385.1\src) 。

| 示例 | 说明 |
|--|--|
| [KMDF 总线驱动程序](/samples/microsoft/windows-driver-samples/sample-kmdf-bus-driver-for-osr-usb-fx2) | 演示如何将 KMDF 用于使用 OSR FX2 设备的总线驱动程序。 |
| [OSR USB-FX2 的示例 KMDF 函数驱动程序](/samples/microsoft/windows-driver-samples/sample-kmdf-function-driver-for-osr-usb-fx2) | 演示如何对 USB 设备执行批量和中断数据传输。 该示例是针对 OSR USB-FX2 学习工具包编写的。 |
| [USB 函数客户端驱动程序](/samples/microsoft/windows-driver-samples/usb-function-client-driver) | 用于演示如何使用 USB 函数类扩展驱动程序 (UFX) 创建 Windows USB 函数控制器驱动程序的主干示例驱动程序。 |
| [适用于 OSR USB-FX2 (UMDF 1) 上方的示例 UMDF 筛选器 ](/samples/microsoft/windows-driver-samples/sample-umdf-filter-above-kmdf-function-driver-for-osr-usb-fx2-umdf-version-1) | 演示如何将一个 UMDF 筛选器驱动程序作为上方筛选器驱动程序加载到 kmdf \_ fx2 示例驱动程序之上。 该示例是针对 OSR USB-FX2 学习工具包编写的。 |
| [适用于 OSR 的 UMDF 函数驱动程序的示例 UMDF 筛选器-FX2 (UMDF 1) ](/samples/microsoft/windows-driver-samples/sample-umdf-filter-above-umdf-function-driver-for-osr-usb-fx2-umdf-version-1) | 演示如何将 UMDF 筛选器驱动程序加载为高于 UMDF \_ fx2 示例驱动程序的上方筛选器驱动程序。 该示例是针对 OSR USB-FX2 学习工具包编写的。 |
| [UMDF 1 函数驱动程序](/samples/microsoft/windows-driver-samples/sample-umdf-function-driver-for-osr-usb-fx2-umdf-version-1) | 适用于 OSR FX2 设备的 User-Mode Driver Framework (UMDF 1) 驱动程序。 它包括测试应用程序和示例设备元数据，并支持模拟和空闲关机。 |
| [UMDF 2 函数驱动程序](/samples/microsoft/windows-driver-samples/sample-function-driver-for-osr-usb-fx2-umdf-version-2) | 适用于 OSR FX2 设备的 User-Mode Driver Framework (UMDF 2) 驱动程序。 它包括测试应用程序和示例设备元数据，并支持模拟和空闲关机。 |
| [Usbsamp 通用 USB 驱动程序](/samples/microsoft/windows-driver-samples/usbsamp-generic-usb-driver) | 演示如何对泛型 USB 设备的大容量和同步终结点执行全速、高速和 SuperSpeed 的传输。 |
| [USBView](/samples/microsoft/windows-driver-samples/usbview-sample-application) | 一个 Windows 应用程序，它允许你浏览系统中的所有 USB 控制器和连接的 USB 设备。 |
| [适用于 OSR 的 WDF 示例驱动程序学习实验室-FX2](/samples/microsoft/windows-driver-samples/wdf-sample-driver-learning-lab-for-osr-usb-fx2) | 包含一个控制台测试应用程序以及一系列适用于 KMDF 和 UMDF 版本1的迭代驱动程序。 |
| [UcmCxUcsi 端口控制器客户端驱动程序](/samples/microsoft/windows-driver-samples/ucmtcpcicx-port-controller-client-driver-v2) | 演示如何使用 USB 连接器管理器类扩展驱动程序 (UcmCx) 创建 Windows USB 类型 C 端口控制器驱动程序。 |
| [UcmTcpciCx 端口控制器客户端驱动程序](/samples/microsoft/windows-driver-samples/ucmtcpcicx-port-controller-client-driver) | 演示如何使用 USB 连接器管理器 Type-C 端口控制器接口类扩展驱动程序 (UcmTcpciCx) 创建 Windows USB 类型 C 端口控制器驱动程序。 |
| [UcmUcsiCx ACPI 客户端驱动程序](/samples/microsoft/windows-driver-samples/ucmucsicx-acpi-client-driver) | 演示如何使用 USB 连接器管理器类扩展驱动程序 (UcmCx) 创建 UCSI 兼容 (ACPI 传输) Windows USB 类型 C 端口控制器驱动程序。 |
