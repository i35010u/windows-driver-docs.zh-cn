---
title: USBCAMD2 功能
description: USBCAMD2 功能
ms.assetid: e800948a-6903-496e-9561-697ff5ccd1d7
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- USBCAMD2 功能 WDK Windows 2000 内核流式处理
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfe47fbc91634a6f1a718bc59e77070fe94265f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562862"
---
# <a name="usbcamd2-features"></a>USBCAMD2 功能


以下功能都位于 USBCAMD2 （原始 USBCAMD 微型驱动程序库不支持这些功能）：

-   **自动完成 Srb**

    USBCAMD2 可以自动完成 Srb。 原始 USBCAMD 需要相机微型驱动程序以完成 Srb。 若要指定 USBCAMD2 自动完成 Srb，请将传递 **，则返回 TRUE**中*NeedsCompletion*参数调用时[ **USBCAMD\_AdapterReceivePacket**](https://msdn.microsoft.com/library/windows/hardware/ff568574)。

-   **对硬件触发的事件，通过中断管道的支持**

    USBCAMD2 照相机微型驱动程序可以注册通过中断管道发送信号的外部触发器事件。 可以由 USBCAMD2 处理中断。 例如，快照按钮被按下时中断管道可以发出信号照相机微型驱动程序。 仍映像 (STI) 体系结构事件监视器可以设备事件的通知。 通过按快照按钮，将通知 STI 监视器以及如何可以使用 STI 推送模型启动以前注册的 STI 应用程序，仍在照像机上，pin 与相关联。 若要配置 USBCAMD2 发送外部触发器事件，请将传递*USBCAMD\_CamControlFlag\_EnableDeviceEvents*标记中*CamControlFlag*参数调用时[ **USBCAMD\_InitializeNewInterface**](https://msdn.microsoft.com/library/windows/hardware/ff568599)。

-   **通用 USB 管道配置支持**

    USBCAMD2 支持使用大容量或为传输视频并仍图像数据等时管道的照相机。 USBCAMD2 查询微型驱动程序，并动态生成在初始化过程中的管道配置信息。 原始 USBCAMD 库假定有关数量或类型的管道使用预设的管道配置信息。 指定管道的配置[ **USBCAMD\_管道\_Config\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff568623)数组传递给[ *CamConfigureEx*](https://msdn.microsoft.com/library/windows/hardware/ff557605)。

-   **将其固定，并捕获 Pin 支持**

    USBCAMD2 可以公开仍固定到*stream.sys*除了捕获 pin 原始 USBCAMD 公开的类。 仍处于 pin 可以公开的成像设备具有任一专用的管道，以仍 pin 或使用相同管道进行多路复用仍和视频插针。 若要公开仍 pin，您可以指定包含 USBCAMD 静止图像数据的管道\_管道\_Config\_描述符数组之前将传递到的数组**CamConfigureEx**。

-   **Plug and Play 和电源管理改进的支持**

    USBCAMD2 Plug and play 在 Windows 2000 和更高版本，如意外删除设备提供支持。 USBCAMD2 还支持在 Windows XP 及更高版本的系统休眠 （休眠支持不是在 Windows 98 与未安装 service pack、 Windows 98 SE 中或 Windows 2000 中出现的） 和 Windows Millennium Edition 和更高版本。

 

 




