---
title: 设备和驱动程序安装路线图
description: 设备和驱动程序安装路线图
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cff8aa558f56241bfdac0e0303e2634d40206104
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824437"
---
# <a name="roadmap-for-device-and-driver-installation"></a>设备和驱动程序安装路线图


![指向地图的罗盘、地图和手指的插图](images/map-hand-sml.png)

若要在 Windows 操作系统中安装设备和驱动程序，请执行以下步骤：

-   步骤1：了解 Windows 中设备和驱动程序安装的基本知识。

    你必须了解 Windows 操作系统系列中的设备和驱动程序安装的基本知识。 这将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关详细信息，请参阅 [设备和驱动程序安装概述](overview-of-device-and-driver-installation.md)。

-   步骤2：了解驱动程序包及其组件。

    驱动程序包由必须提供的用于安装设备并支持 Windows 的所有组件组成。

    若要安装设备或驱动程序，您必须具有系统提供的组件和供应商提供的组件。 系统为所有设备类提供通用安装软件。 供应商必须在驱动程序包中提供一个或多个设备特定组件。

    有关详细信息，请参阅 [驱动程序包](driver-packages.md)。

-   步骤3：了解 (INF) 文件的信息。

    INF 文件包含系统提供的 [设备安装组件](/previous-versions/ff541277(v=vs.85)) 用来安装 [驱动程序包](driver-packages.md)的信息和设备设置，如设备的驱动程序和任何设备特定的应用程序。

    有关详细信息，请参阅 [INF 文件](overview-of-inf-files.md)。

-   步骤4：为你的设备和驱动程序创建驱动程序包。

    驱动程序包必须提供 INF 文件、设备的驱动程序文件，还可以选择提供其他软件组件。 可以参考示例 Toaster 驱动程序包来确定驱动程序包所需的组件。

    有关驱动程序包的组件的详细信息，请参阅 [创建驱动程序包](../develop/creating-a-driver-package.md)。

    有关驱动程序包的详细信息，请参阅 [Toaster 示例](../wdf/sample-kmdf-drivers.md)。

-   步骤5：在开发和测试期间对驱动程序包进行测试。

    测试签名是指使用测试证书对要在测试计算机上使用的 [驱动程序包](driver-packages.md) 的预发布版本进行签名。 具体而言，这允许开发人员使用自签名证书（如 [**MakeCert**](../devtest/makecert.md) 工具生成的证书）对驱动程序包进行签名。 此功能使开发人员能够在启用了驱动程序签名验证的情况下安装和测试 Windows 中的驱动程序包。

    有关详细信息，请参阅 [在开发和测试期间对驱动程序进行签名](./introduction-to-test-signing.md)。

- 步骤6：对驱动程序包进行发布签名以进行分发。

    测试并验证 [驱动程序包](driver-packages.md)后，应对驱动程序包进行发布签名。 版本签名标识驱动程序包的发行者。 尽管此步骤是可选的，但驱动程序包应该出于以下原因进行发布签名：

  - 确保驱动程序包的可靠性、完整性和可靠性。 Windows 使用数字签名来验证发行者的身份，并验证自发布后该驱动程序是否已更改。
  - 通过促进自动驱动程序安装，提供最佳用户体验。
  - 在64位版本的 Windows Vista 和更高版本的 Windows 上运行内核模式驱动程序。
  - 播放特定类型的下一代高级内容。

    [驱动程序包](driver-packages.md) 通过以下任一方式进行版本签名：

  - 通过[Windows 硬件兼容性计划](/windows-hardware/design/compatibility/)获取的[WHQL 版本签名](whql-release-signature.md) (适用于 windows 10) 或 windows[硬件认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) (适用于 windows 8/8.1 和更早版本的操作系统) 。
  - 通过软件发行者证书创建的发布签名 [ (SPC) ](software-publisher-certificate.md)。

    有关详细信息，请参阅 [签署公用版驱动程序](signing-drivers-for-public-release--windows-vista-and-later-.md)。

- 步骤7：分发驱动程序包。

    最后一步是分发 [驱动程序包](driver-packages.md)。 如果你的驱动程序包满足适用于 windows 10) 的 [Windows 硬件兼容性计划](/windows-hardware/design/compatibility/) (中定义的质量标准，或者 windows 8/8.1 及更早版本的) 操作系统 (的 [Windows 硬件认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) ，则可以通过 Microsoft Windows 更新程序进行分发。 有关详细信息，请参阅 [将驱动程序发布到 Windows 更新](../dashboard/publish-a-driver-to-windows-update.md)。

这些是基本步骤。 根据单个设备和驱动程序的安装需要，可能需要执行其他步骤。
