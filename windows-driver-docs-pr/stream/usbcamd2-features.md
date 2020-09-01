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
ms.openlocfilehash: 23cac2131e50d003f129eaeb232223f844a808a4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185529"
---
# <a name="usbcamd2-features"></a>USBCAMD2 功能


USBCAMD2 中存在以下功能 (原始 USBCAMD 微型驱动程序库不支持这些功能) ：

-   **SRBs 自动完成**

    USBCAMD2 可以自动完成 SRBs。 原始 USBCAMD 必需的相机微型驱动程序完成 SRBs。 若要指定 USBCAMD2 自动完成 SRBs，请在调用[**USBCAMD \_ AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)时在*NeedsCompletion*参数中传递**TRUE** 。

-   **通过中断管道支持硬件触发的事件**

    USBCAMD2 摄像微型驱动程序可以注册通过中断管道发出信号的外部触发器事件。 中断可以由 USBCAMD2 处理。 例如，当按下快照按钮时，中断管道可以向照相机发出信号微型驱动程序信号。 仍可 (STI) 体系结构事件监视器的静止映像，通知设备事件。 通过按 "快照" 按钮，可以使用 STI 推送模式，通知 STI 监视器，并使用推送模型来启动先前注册的 STI 应用程序，该应用程序与相机上的静止 pin 相关联。 若要将 USBCAMD2 配置为发送外部触发器事件，请在调用[**CamControlFlag \_ USBCAMD**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)时传递*InitializeNewInterface*参数中的*USBCAMD \_ CamControlFlag \_ EnableDeviceEvents*标志。

-   **多功能 USB 管道配置支持**

    USBCAMD2 支持使用大容量或同步管道传输视频和静态图像数据的照相机。 USBCAMD2 在初始化期间查询微型驱动程序并动态生成管道配置信息。 原来的 USBCAMD 库假定预设的管道配置信息与所使用的管道的数量或类型有关。 可以在传递给[*CamConfigureEx*](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)的[**USBCAMD \_ 管道配置 \_ \_ 描述符**](/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)数组中指定管道配置。

-   **仍支持 Pin 并捕获 Pin 支持**

    除了原始 USBCAMD 公开的捕获 pin 外，USBCAMD2 还可公开 *stream.sys* 类的静止 pin。 对于具有专用管道以进行静止插针或使用相同管道来多路复用静止和视频 pin 的图像设备，可以公开静止 pin。 若要公开静态静态，请在将 \_ \_ \_ 数组传递给 **CAMCONFIGUREEX**之前指定包含 USBCAMD 管道配置描述符数组中的静止图像数据的管道。

-   **改进了对即插即用和电源管理的支持**

    USBCAMD2 支持 Windows 2000 及更高版本中的即插即用，如意外删除设备。 USBCAMD2 还支持 Windows XP 和更高版本中的系统休眠 (不会在 Windows 98 中提供休眠支持，没有安装 service pack、Windows 98 SE 或 Windows 2000) 和 Windows Millennium Edition 及更高版本。

 

