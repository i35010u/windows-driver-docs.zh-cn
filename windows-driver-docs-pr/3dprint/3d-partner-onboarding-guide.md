---
title: 3D 打印合作伙伴加入指南
description: 本主题介绍如何实现 Windows 更新上发布的3D 打印机驱动程序。
ms.date: 05/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5bf0c671a5878bb93e375c967fdb5527fa93759c
ms.sourcegitcommit: 32f42241991d57032e5d39ee9f2a3ab4a66ae396
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/18/2020
ms.locfileid: "83553330"
---
# <a name="3d-print-partner-onboarding-guide"></a>3D 打印合作伙伴加入指南

加入 Microsoft 3D 打印生态系统使3D 打印机制造商能够在 Windows 10 上提供出色的即插即用体验。 此策略将消除用户在查找和手动安装驱动程序时遇到的问题。 此外，Windows 更新确保用户始终使用最新的设备驱动程序，并获得最佳体验。

## <a name="3d-print-driver-overview"></a>3D 打印驱动程序概述

Windows 10 上的即插即用3D 打印机是通过 Windows 更新上发布的一对驱动程序实现的：

### <a name="upper-driver-render-filter"></a>上层驱动程序（呈现筛选器）

- 实现切片器。 驱动程序将[3MF](https://3mf.io/)作为输入，并生成 G 代码或其他类似计算机级别的数据。

- 创建打印队列。 设备显示在 "**设备和打印机**" 下，在 " **3D 打印" 对话框**中用于兼容的[3d 打印应用程序](https://developer.microsoft.com/windows/hardware/3d-print/software-partners)。

### <a name="lower-driver-usb-driver"></a>更低的驱动程序（USB 驱动程序）

- 实现无线协议（通常为 USB 串行协议或本机 USB）

- 内核模式驱动程序 \\ 为上部驱动程序创建 ENUM 3DPRINTER 设备节点

- 用户模式组件（合作伙伴 DLL）将 G 代码发送到设备

- 报告设备功能、作业状态和实现作业取消

- 安装3D 打印服务和3D 端口监视器（3dmon）

## <a name="choosing-the-right-driver-model"></a>选择适当的驱动程序模型

![显示 Microsoft 与自定义3D 驱动程序模型的优点和缺点的4x4 网格，如以下部分中所述](images/onboarding-driver-models.png)

## <a name="3d-print-driver-with-custom-slicer"></a>带有自定义切片器的3D 打印驱动程序

1. 获取并验证设备 USB 硬件 ID

    - 确保设备固件具有由[Usb 实现者论坛（usb-IF）](https://www.usb.org/)分配的唯一供应商 ID 和产品 ID （VID/PID）。 对于 USBSER 设备，强烈建议使用唯一序列号来防止 USB 端口更改发生冲突。

2. 安装 Microsoft 工具和 Sdk

    - 下载并安装[Visual Studio 社区版](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community)

    - 下载并安装[Windows 10 SDK](https://developer.microsoft.com/en-US/windows/downloads/windows-10-sdk/)

    - 下载并安装[3d 打印 SDK](https://go.microsoft.com/fwlink/p/?LinkId=394375)

   > [!NOTE]
   > 3D 打印 SDK 将安装在 C： \\ Program Files （x86） \\ Microsoft Sdk \\ 3d 打印中。

3. 实现 USB 驱动程序

    - 制造商可以通过创建合作伙伴 DLL 来使用其3D 打印机的 Microsoft USB 驱动程序。 有关详细信息，请参阅[3d 打印机自定义 USB 接口支持](3d-printer-custom-usb-interface.md)。

    - 如果打印机使用 Microsoft 切片器，则其创建的硬件 ID 必须是**枚举 \\ 3DPrint \\ MS3DPrint**

    > [!NOTE]
    > 如果打印机使用自定义切片器，则继续执行步骤4-7。

4. 构建 Fabrikam 驱动程序（仅限切片器模板）

    - 构建并获取驱动程序包。 这会创建包含切片器部分的 x64 文件夹。

5. 添加自定义切片器

    - 修改 cpp 文件，使其包括：

      - 3MF 分析器（使用 Windows 10 版本 1607 3MF API）

      - 编写 G 代码

6. 添加打印机节点

    - 在 Fabrikam 打印驱动程序中打开 inf

    - 替换项硬件 Id：

        ```INF
        %DeviceName%=FabrikamPrintDriverV4\_Install,3DPRINTER\\Fabrikam1

        %DeviceNamePlus%=FabrikamPrintDriverV4\_Install,3DPRINTER\\Fabrikam2

        DeviceName="CONTOSO FABRIKAM 1"

        DeviceNamePlus="CONTOSO FABRIKAM 2"
        ```

7. 发布和分发驱动程序

    - 按照[Windows 合作伙伴中心](https://docs.microsoft.com/windows-hardware/drivers/dashboard)主题中的指导进行操作以发布驱动程序。
