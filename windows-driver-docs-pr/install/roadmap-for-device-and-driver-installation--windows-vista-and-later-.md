---
title: 设备和驱动程序安装路线图
description: 设备和驱动程序安装路线图
ms.assetid: d6cb6d8c-226f-4b6f-989a-36184236f826
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 829b5049c9e3d314e6b38ea239c9b7040fe639e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382271"
---
# <a name="roadmap-for-device-and-driver-installation"></a>设备和驱动程序安装路线图


![示意图，指南针，一个映射，以及指向映射手指](images/map-hand-sml.png)

若要在 Windows 操作系统中安装的设备和驱动程序，请按照下列步骤：

-   第 1 步：了解设备和驱动程序安装在 Windows 中的基础知识。

    你必须了解设备和驱动程序安装在 Windows 系列操作系统中的基础知识。 这将帮助您做出适当的设计决策，并可简化开发过程。 有关详细信息，请参阅[概述的设备和驱动程序安装](overview-of-device-and-driver-installation.md)。

-   步骤 2：了解有关驱动程序包及其组件。

    必须提供安装你的设备，并支持在 Windows 下的所有组件的包含驱动程序包。

    若要安装的设备或驱动程序，必须具有系统提供和供应商提供的组件。 系统提供的所有设备类的通用安装软件。 供应商必须提供的驱动程序包中的一个或多个特定于设备的组件。

    有关详细信息，请参阅[驱动程序包](driver-packages.md)。

-   步骤 3:了解有关信息 (INF) 文件。

    INF 文件包含的信息和设备设置的系统提供[设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))使用来安装你[驱动程序包](driver-packages.md)，如设备以及任何驱动程序特定于设备的应用程序。

    有关详细信息，请参阅[INF 文件](overview-of-inf-files.md)。

-   步骤 4：创建你的设备和驱动程序的驱动程序包。

    驱动程序包必须提供一个 INF 文件，设备的驱动程序文件，以及 （可选） 提供额外的软件组件。 还可以参考示例 Toaster 驱动程序包，以确定哪些组件所需的驱动程序包。

    驱动程序包的组件的详细信息，请参阅[创建驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/develop/creating-a-driver-package)。

    有关驱动程序包的详细信息，请参阅[Toaster 示例](https://docs.microsoft.com/windows-hardware/drivers/wdf/sample-kmdf-drivers)。

-   步骤 5：在开发和测试期间测试登录您的驱动程序的包。

    测试签名是指使用测试证书进行签名的预发布版本[驱动程序包](driver-packages.md)以用于测试计算机。 具体而言，这允许开发人员通过使用自签名的证书，如签署驱动程序包[ **MakeCert** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/makecert)工具生成。 此功能允许开发人员若要安装和测试驱动程序包在 Windows 中启用驱动程序签名验证。

    有关详细信息，请参阅[签名驱动程序开发和测试期间](signing-drivers-during-development-and-test.md)。

- 步骤 6：发布登录您的驱动程序分发的包。

    已测试并验证后你[驱动程序包](driver-packages.md)，应发布签名的驱动程序包。 版本签名标识驱动程序包的发布服务器。 尽管此步骤是可选的驱动程序的包应为版本签名出于以下原因：

  - 请确保真实性、 完整性和可靠性的驱动程序包。 Windows 使用数字签名来验证发布服务器的身份并验证该驱动程序发布以来未被修改。
  - 通过促进自动驱动程序安装可提供最佳用户体验。
  - 在 64 位版本的 Windows Vista 和更高版本的 Windows 上运行内核模式驱动程序。
  - 播放某些类型的下一代高级内容。

    [驱动程序包](driver-packages.md)是通过已发布签名：

  - 一个[WHQL 版本签名](whql-release-signature.md)通过获得[Windows 硬件兼容性计划](https://docs.microsoft.com/windows-hardware/design/compatibility/)（适用于 Windows 10)，或[Windows 硬件认证计划](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))（适用于Windows 8/8.1 和较旧操作系统）。
  - 通过创建版本签名[软件发布者证书 (SPC)](software-publisher-certificate.md)。

    有关详细信息，请参阅[公开发布的版本的签名驱动程序](signing-drivers-for-public-release--windows-vista-and-later-.md)。

- 步骤 7：将分发驱动程序包。

    最后一步是分发[驱动程序包](driver-packages.md)。 驱动程序包是否满足中定义的质量标准[Windows 硬件兼容性计划](https://docs.microsoft.com/windows-hardware/design/compatibility/)（适用于 Windows 10)，或[Windows 硬件认证计划](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))(适用于 Windows 8 /8.1 和更低版本操作系统），你可以将其分配通过 Microsoft Windows 更新计划。 有关详细信息，请参阅[发布到 Windows 更新的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)。

这些是基本步骤。 其他步骤可能需要基于单个设备和驱动程序的安装要求。
