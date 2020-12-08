---
title: 对驱动程序包进行发布签名
description: 对驱动程序包进行发布签名
keywords:
- 驱动程序签名 WDK，驱动程序包
- 对驱动程序进行签名 WDK，驱动程序包
- 数字签名 WDK，驱动程序包
- 签名 WDK，驱动程序包
- CAT 文件
- .cat 文件
- 目录文件 WDK 驱动程序签名，发布签名
- 公共版本驱动程序签名 WDK，关于发布签名
- release 签名 WDK，关于发布签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da37939cb3150b8092bc9ec19d10140bc7b9b7bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791727"
---
# <a name="release-signing-driver-packages"></a>对驱动程序包进行发布签名


在本部分中，在 Windows Vista 和更高版本的 Windows 上对发布的驱动程序进行签名的计算机称为 *签名计算机*。 签名计算机必须运行 Windows XP SP2 或更高版本的 Windows 操作系统。 例如，可在运行 Windows Vista 的计算机上登录用于 Windows 7 上的发布的驱动程序。

此外，签名计算机必须安装 [驱动程序签名工具](../devtest/tools-for-signing-drivers.md) 。

**注意**  您必须使用 Windows Vista 和更高版本的 Windows 驱动程序工具包 (WDK) 中提供的 [**SignTool**](../devtest/signtool.md) 工具版本。 此工具的早期版本不支持 Windows Vista 和更高版本的 Windows 的内核模式代码签名策略。

 

若要符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 和即插即用 (PnP) windows Vista 和更高版本的 [设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) ，请根据驱动程序的类型为 release 签署一个驱动程序。

**注意**   Windows 代码签名策略要求将驱动程序的签名 [目录文件](catalog-files.md) 安装在系统组件和驱动程序数据库中。 PnP 设备安装会在驱动程序数据库中自动安装 PnP 驱动程序的编录文件。 但是，如果使用已签名的目录文件对非 PnP 驱动程序进行签名，则安装驱动程序的安装应用程序还必须在驱动程序数据库中安装目录文件。

 

### <a name="pnp-kernel-mode-boot-start-driver"></a><a href="" id="pnp-kernel-mode-boot-start-driver"></a> PnP Kernel-Mode Boot-Start 驱动程序

若要符合 Windows Vista 和更高版本的 windows 版本的 [内核模式代码签名64策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) ，请在 *启动启动驱动程序* 文件中嵌入签名，如下所示：

1.  使用软件发行者证书对[驱动程序文件进行发布签名](release-signing-a-driver-file.md) [ (SPC) ](software-publisher-certificate.md)。

2.  [验证驱动程序文件的 SPC 签名](verifying-the-signature-of-a-release-signed-driver-file.md)。

从 Windows Vista 开始，在 *启动启动驱动程序* 文件中嵌入签名对于32位版本的 Windows 是可选的。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入签名，但不需要嵌入的签名。

若要符合 Windows Vista 和更高版本的 Windows 的 [PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) ，你必须获取已签名的 [目录文件](catalog-files.md) 或对 [驱动程序包](driver-packages.md)的编录文件进行签名。 如果驱动程序文件还将包含嵌入的签名，则在对驱动程序包的目录文件进行签名之前，将签名嵌入驱动程序文件中。

如果 [硬件认证工具包 (HCK) ](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) 包含驱动程序的测试程序，请获取驱动程序包的 [WHQL 版本签名](whql-release-signature.md) 。 如果 HCK 没有适用于该驱动程序的测试程序，请 [创建一个编录文件](creating-a-catalog-file-for-a-pnp-driver-package.md) ，并按如下所示对该 [目录文件](catalog-files.md) 进行签名：

**为64位版本的目录文件签名**

可以按如下所示为64位操作系统的目录文件签名：

1.  使用[SPC 签署目录文件](signing-a-catalog-file-with-an-spc.md)，该文件用于在驱动程序文件中嵌入签名。

2.  [验证编录文件的 SPC 签名](verifying-the-spc-signature-of-a-catalog-file.md)。 您可以验证目录文件的签名，也可以验证目录文件中单个文件项的签名。

**为32位版本的目录文件签名**

您可以使用 SPC 为 [目录文件](catalog-files.md) 签名，如64位版本部分中所述，或使用 [商业发布证书](commercial-release-certificate.md) 进行签名，如下所示：

1.  [使用商业版本证书对目录文件进行签名](signing-a-catalog-file-with-a-commercial-release-certificate.md)。

2.  [验证目录文件的签名](verifying-the-signature-of-a-catalog-file-signed-by-a-commercial-relea.md)。 您可以验证目录文件的签名，也可以验证目录文件中单个文件项的签名。

### <a name="non-pnp-kernel-mode-boot-start-driver"></a><a href="" id="non-pnp-kernel-mode-boot-start-driver"></a> Boot-Start 驱动程序的非 PnP Kernel-Mode

若要符合 Windows Vista 和更高版本的 windows 版本的内核模式代码签名64策略，请将签名嵌入 *启动驱动程序* 文件中，如下所示：

1.  [发布-使用 SPC 对驱动程序文件进行签名](release-signing-a-driver-file.md) 。

2.  [验证驱动程序文件的 SPC 签名](verifying-the-signature-of-a-release-signed-driver-file.md)。

从 Windows Vista 开始，在 *启动启动驱动程序* 文件中嵌入签名对于32位版本的 Windows 是可选的。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入签名，但不需要嵌入的签名。

PnP 设备安装签名要求不适用于非 PnP 驱动程序。

### <a name="pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a><a href="" id="pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> 不是 Boot-Start 驱动程序的 PnP Kernel-Mode 驱动程序

64位版本的 Windows Vista 和更高版本的 Windows 上的内核模式代码签名策略不需要非引导 PnP 驱动程序具有嵌入签名。 但是，如果驱动程序文件将包含嵌入的签名，则在对[驱动程序包的](driver-packages.md)[目录文件](catalog-files.md)进行签名之前，将签名嵌入驱动程序文件中。

若要符合 PnP 设备安装签名要求，你必须获取已签名的目录文件或对驱动程序包的编录文件进行签名。

如果 [硬件认证工具包 (HCK) ](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) 包含驱动程序的测试程序，请获取驱动程序包的 [WHQL 版本签名](whql-release-signature.md) 。 如果 HCK 没有驱动程序的测试 [程序，请](creating-a-catalog-file-for-a-pnp-driver-package.md) 按照本部分中所述的相同方式，使用此部分中所述的方式对 [目录](catalog-files.md) 文件进行签名，以便对 PnP 内核模式 *启动驱动程序* 的编录文件进行签名。

### <a name="non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a><a href="" id="non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> 不是 Boot-Start 驱动程序的非 PnP Kernel-Mode 驱动程序

若要符合64位版本 Windows Vista 和更高版本的 Windows 的内核模式代码签名策略，请在驱动程序文件中嵌入签名，或为 [驱动程序包](driver-packages.md)签名目录文件。

从 Windows Vista 开始，将签名嵌入驱动程序文件对于32位版本的 Windows 是可选的。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入签名，但不需要嵌入的签名。

PnP 设备安装签名要求不适用于非 PnP 驱动程序。

**注意**   使用嵌入的签名通常比使用已签名的目录文件更简单、更有效。 有关使用嵌入的签名与签名的目录文件的优点和缺点的详细信息，请参阅对 [驱动程序进行测试签名](../develop/signing-a-driver.md)。

 

若要在非 PnP 内核模式驱动程序的文件中嵌入版本签名，而该驱动程序不是 *启动启动驱动* 程序，请执行以下步骤：

1.  使用 SPC[对驱动程序文件进行签名](release-signing-a-driver-file.md)。

2.  [验证驱动程序文件的签名](verifying-the-signature-of-a-release-signed-driver-file.md)。

若要为非 PnP 内核模式驱动程序（不是 *启动启动驱动程序*）发布目录文件，请执行以下步骤：

1.  [为非 PnP 驱动程序创建目录文件](creating-a-catalog-file-for-a-non-pnp-driver-package.md)。

2.  [使用 SPC 对编录文件进行签名](signing-a-catalog-file-with-an-spc.md)。

3.  [验证编录文件的 SPC 签名](verifying-the-spc-signature-of-a-catalog-file.md)。

如果此类型的驱动程序具有已签名的 [目录文件](catalog-files.md) 而不是嵌入的签名，则安装驱动程序的安装应用程序必须在系统组件和驱动程序数据库中安装目录文件。 有关详细信息，请参阅为 [非 PnP 驱动程序安装 Release-Signed 编录文件](installing-a-release-signed-catalog-file-for-a-non-pnp-driver.md)。
