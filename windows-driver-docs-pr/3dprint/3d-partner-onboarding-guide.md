---
title: 3D 打印合作伙伴加入指南
description: 本主题介绍如何在 Windows 更新上实现 3D 打印机驱动程序，然后发布。
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0a923651df76199d8ff6179c1475c271ebad2e33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576960"
---
# <a name="3d-print-partner-onboarding-guide"></a>3D 打印合作伙伴加入指南

加入 Microsoft 3D 打印生态系统使 3D 打印机制造商提供 Windows 10 上完美的即插即用播放体验。 此策略中删除用户查找和手动安装驱动程序时遇到的问题的可能性。 此外，Windows 更新可确保用户始终使用其设备的最新驱动程序和获得可用的最佳体验。

## <a name="3d-print-driver-overview"></a>3D 打印驱动程序概述

通过 Windows 更新上发布的驱动程序的一对实现 Windows 10 上的即插即用 play 3D 打印机：

### <a name="upper-driver-render-filter"></a>上部驱动程序 （呈现筛选器）

- 实现切片器。 驱动程序采用[3MF](http://www.3mf.io)作为输入，生成 G 代码或其他类似的计算机级数据。

- 创建打印队列。 该设备将显示下**设备和打印机**并在**3D 打印对话框**为兼容[3D 打印应用程序](https://developer.microsoft.com/windows/hardware/3d-software-partners)。

### <a name="lower-driver-usb-driver"></a>较低的驱动程序 （USB 驱动程序）

- 实现绑定协议 （通常 USB 串行或本机 USB）

- 内核模式驱动程序创建枚举\\3DPRINTER 设备节点的上部的驱动程序

- 用户模式组件 (合作伙伴 DLL) 将 G 代码发送到设备

- 报告设备功能、 作业状态和实现作业取消

- 安装 3D 打印服务和 3D 端口监视器 (3dmon)

## <a name="choosing-the-right-driver-model"></a>选择合适的驱动程序模型

![显示 Microsoft 和自定义的 3D 驱动程序模型的优点和缺点的上限的 4x4 网格，并减少驱动程序下, 一节中所述](images/onboarding-driver-models.png)

## <a name="3d-print-driver-with-custom-slicer"></a>3D 打印驱动程序和使用自定义切片器

1. 获取并验证设备 USB 硬件 ID

    - 请确保设备固件具有唯一供应商 ID 和产品 ID (VID/PID) 由分配[USB 实现论坛 (USB-如果)](http://www.usb.org)。 对于 USBSER 设备，我们强烈建议使用唯一的序列号以防止冲突在 USB 端口的更改。

2. 安装 Microsoft 工具和 Sdk

    - 下载并安装[Visual Studio Community Edition](https://go.microsoft.com/fwlink/p/?LinkId=534599)

    - 下载并安装[Windows 10 SDK](https://go.microsoft.com/fwlink/p/?LinkID=822845)

    - 下载并安装[3D 打印 SDK](https://go.microsoft.com/fwlink/p/?LinkId=394375)

   > [!NOTE]
   > 3D 打印 SDK 将安装在 c:\\Program Files (x86)\\Microsoft Sdk\\3D 打印。

3. 实现 USB 驱动程序

    - 制造商可以通过创建合作伙伴 DLL 为其 3D 打印机使用 Microsoft USB 驱动程序。 有关详细信息，请参阅[3D 打印机自定义 USB 接口支持](3d-printer-custom-usb-interface.md)。

    - 如果打印机正在使用 Microsoft 切片器，它将创建的硬件 ID 必须是**Enum\\3DPrint\\MS3DPrint**

    > [!NOTE]
    > 如果打印机正在使用自定义切片器，继续执行步骤 4-7。

4. 生成 Fabrikam 驱动程序 （仅限切片器模板）

    - 生成并获取该驱动程序程序包。 这将创建 x64 文件夹与切片器部分。

5. 添加自定义切片器

    - 修改 cpp 文件，包括：

      - 3MF 分析器 （使用 Windows 10 版本 1607年 3MF API）

      - 编写 G 代码

6. 添加的打印机节点

    - 在 Fabrikam 打印驱动程序中打开 inf

    - 替换条目硬件 Id:

        ```INF
        %DeviceName%=FabrikamPrintDriverV4\_Install,3DPRINTER\\Fabrikam1

        %DeviceNamePlus%=FabrikamPrintDriverV4\_Install,3DPRINTER\\Fabrikam2

        DeviceName="CONTOSO FABRIKAM 1"

        DeviceNamePlus="CONTOSO FABRIKAM 2"
        ```

7. 发布和分发该驱动程序

    - 遵循中的指导[Windows 合作伙伴中心](https://docs.microsoft.com/windows-hardware/drivers/dashboard)主题发布您的驱动程序。
