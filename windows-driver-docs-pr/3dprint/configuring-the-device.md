---
title: 配置设备
description: 若要配置该设备，你应该在 "设备和打印机" 控制面板中拥有一个3D 打印机设备，并可使用 Microsoft 切片器打印到 G 代码。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b38376d1e946b72ad8b5ecb98b682ea28ac4a8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783633"
---
# <a name="configuring-the-device"></a>配置设备


若要配置该设备，你应该在 " **设备和打印机** " 控制面板中拥有一个3d 打印机设备，并可使用 Microsoft 切片器打印到 G 代码。

接下来，需要在配置文件中更改切片器和高级设置。

有两个配置文件控制打印机属性和切片器设置。

打印到硬件设备时： 

- **C： \\Windows \\ System32 \\ MS3DPrint \\ StandardGCode \* 。XML** –此参数由 StandardGCode.DLL 使用，可以从设备更改为设备，具体取决于下面的 **配置 xml** 项中定义的注册表映射：

    - 每个打印机队列： HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 枚举 \\ 3DPRINTER \\ {PrinterName} \\ {node}

    - 每个硬件 ID： HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 枚举 \\ USB \\ {VID&PID} \\ {DeviceSerial} \\ 设备参数\\

打印到文件时 (不存在任何 USB 驱动程序) ：

- **C： \\Windows \\ System32 \\ 假脱机 \\ 驱动程序 \\ x64 \\ 3 \\MS3DPrinterDeviceConfig.xml** –这是由切片器全局使用并使用的。

为简单起见，请以 **管理员身份** 编辑 **MS3DPrinterDeviceConfig.xml** 文件（如果使用的是 "**打印到文件**" 功能） (G-代码文件) 未连接任何物理设备，并且在打印到物理设备时编辑 **StandardGCode.XML** 。

现在，你已准备好从 Windows 中的3D 生成器应用之类的应用程序或任何实现 Windows native 3D 打印的应用商店或桌面应用程序进行三维打印。

 

 




