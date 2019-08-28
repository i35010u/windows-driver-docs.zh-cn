---
title: 示例 UMDF 驱动程序
description: 本主题列出了可从 GitHub 上的 Windows 驱动程序示例存储库中下载的可用用户模式驱动程序框架 (UMDF) 示例驱动程序。
ms.assetid: 9C8576E1-4CC7-4A7E-A822-C6BBFDC7482D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 900f3efafeb4f5b64c39c439bbbb51cea0c4089d
ms.sourcegitcommit: 44f09d983954f27fd90b737a2dd142aad7dffd9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70059176"
---
# <a name="sample-umdf-drivers"></a>示例 UMDF 驱动程序

本主题列出了可以在[Microsoft 示例门户](https://docs.microsoft.com/samples/browse/?products=windows-wdk)上浏览和下载的可用用户模式驱动程序框架 (UMDF) 示例驱动程序。 你还可以在 GitHub 上克隆、分叉或下载[Windows 驱动程序-示例](https://github.com/Microsoft/Windows-driver-samples)存储库。

旧版本的驱动程序示例存档在[Windows 8.1 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)中

## <a name="umdf-2-samples"></a>UMDF 2 示例

-   [OSR FX2 的示例函数驱动程序 (UMDF 版本 2)](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/umdf2_fx2)
-   [Toaster 示例 (UMDF 版本 2)](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/umdf2)
-   [回显示例 (UMDF 版本 2)](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/umdf2)
-   [Power Framework (PoFx) 示例 (UMDF 版本 2)](https://github.com/Microsoft/Windows-driver-samples/tree/master/pofx/UMDF2)

## <a name="umdf-1-samples"></a>UMDF 1 示例

-   [GPIO 示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/gpio/samples)
-   Windows 8.1 中移除了 HID 客户端示例驱动程序 (Fx2Hid) 示例。 如果你正在编写与 HID 设备通信的通用 Windows 应用, 你将使用 Windows 自定义命名空间直接访问设备的 HID 集合。 有关详细信息, 请参阅[自定义驱动程序访问](https://go.microsoft.com/fwlink/p/?LinkId=618584)示例应用和[HidUsbFx2](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/hidusbfx2)示例驱动程序。 如果要编写访问 HID 集合的 Win32 应用程序, 请参阅[HClient 示例应用程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/hclient)。
-   [近字段近程示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/nfp/net)
-   [用于 OSR USB-FX2 的 KMDF 函数驱动程序之上的示例 UMDF 筛选器驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/umdf_filter_kmdf)
-   [OSR USB 的示例 UMDF 函数驱动程序-FX2](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/umdf_fx2)
-   [SkeletonI2C 示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/spb/SkeletonI2C)
-   [Toaster](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv)
-   [UMDF 驱动程序主干示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/umdfSkeleton)
-   [UMDF 回显示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/umdf)
-   [UMDF SocketEcho 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/umdfSocketEcho)
-   [虚拟串行驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/VirtualSerial)
-   [Windows 生物识别驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics)
-   [WPD 基本-硬件示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/wpd/WpdBasicHardwareDriver)
-   [WPD 多传输示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/wpd/WpdMultiTransportDriver)
-   [WPD 服务示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/wpd/WpdServiceSampleDriver)
-   [WPD WUDF 示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/wpd/WpdWudfSampleDriver)
-   [适用于便携设备的 WPDHelloWorld 示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/wpd/WpdHelloWorldDriver)
