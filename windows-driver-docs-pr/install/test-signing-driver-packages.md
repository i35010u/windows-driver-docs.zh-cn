---
title: 对驱动程序包进行测试签名
description: 对驱动程序包进行测试签名
ms.assetid: 84727762-5ba0-48ea-8d5a-7ac54aadbb7e
keywords:
- 驱动程序签名 WDK，驱动程序包
- 对驱动程序进行签名 WDK，驱动程序包
- 数字签名 WDK，驱动程序包
- 签名 WDK，驱动程序包
- 驱动程序包数字签名 WDK
- 包数字签名 WDK
- 测试签名驱动程序 WDK，驱动程序包
- 测试签名驱动程序包 WDK
- 测试签名驱动程序包 WDK，关于测试签名驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d961b8c8b3d1e6e94070289a8fe3c938a867cb1d
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361355"
---
# <a name="test-signing-driver-packages"></a>对驱动程序包进行测试签名


在本部分中，在 Windows Vista 和更高版本的 Windows 上测试用于发布的驱动程序的计算机称为 *签名计算机* 。 签名计算机必须运行 Windows XP SP2 或更高版本的 Windows。 例如，可在运行 Windows Vista 的计算机上登录用于 Windows 7 上的发布的驱动程序。

为了使用 [驱动程序签名工具](../devtest/tools-for-signing-drivers.md)，签名计算机必须安装了 Windows Vista 和更高版本的 WDK。

**注意**  您必须使用 Windows Vista 和更高版本的 Windows 驱动程序工具包 (WDK) 中提供的 [**SignTool**](../devtest/signtool.md) 工具版本。 早期版本的 SignTool 不支持 Windows Vista 和更高版本的 Windows 的内核模式代码签名策略。

 

为了符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 和 [即插即用 (PnP) ](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) windows Vista 和更高版本的 windows 安装签名要求，你必须在开发和测试该驱动程序的过程中对驱动程序进行签名。 根据驱动程序类型，可以按如下所示对签名计算机上的驱动程序进行签名。

**注意**  Windows 代码签名策略要求在系统组件和驱动程序数据库中安装 [驱动程序包](driver-packages.md)的签名 [目录文件](catalog-files.md)。 PnP 设备安装会在驱动程序数据库中自动安装 PnP 驱动程序的编录文件。 但是，如果使用已签名的目录文件对非 PnP 驱动程序进行签名，则安装驱动程序的安装应用程序还必须在驱动程序数据库中安装目录文件。

 

### <a name="pnp-kernel-mode-boot-start-driver"></a><a href="" id="pnp-kernel-mode-boot-start-driver"></a> PnP Kernel-Mode Boot-Start 驱动程序

若要符合 Windows Vista 和更高版本的 windows 版本的内核模式代码签名64策略，请在 *启动启动驱动程序* 文件中嵌入签名，如下所示：

1.  对[驱动程序文件进行测试签名](test-signing-a-driver-file.md)。

2.  [验证测试签名驱动程序文件的签名](verifying-the-signature-of-a-test-signed-driver-file.md)。

从 Windows Vista 开始，在 *启动启动驱动程序* 文件中嵌入签名对于32位版本的 Windows 是可选的。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入签名，但不需要嵌入签名。

为了符合 Windows Vista 和更高版本的 Windows 的[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)，你还必须对[驱动程序包](driver-packages.md)的[目录文件](catalog-files.md)进行测试签名。 如果驱动程序文件还将包含嵌入的签名，则在对驱动程序包的目录文件进行签名之前，将签名嵌入驱动程序文件中。

你可以提交请求，让 [Windows 硬件质量实验室 (WHQL) ](whql-test-signature-program.md) 对 [编录文件](catalog-files.md)进行测试签名。 或者，你可以使用测试证书自行测试目录文件，如下所示：

1.  [创建编录文件](creating-a-catalog-file-for-a-test-signed-driver-package.md)。

2.  [对编录文件进行测试签名](test-signing-a-catalog-file.md)。

3.  [验证测试签名的目录文件的签名](verifying-the-signature-of-a-test-signed-catalog-file.md)。

    您可以验证目录文件本身的签名，还是在目录文件中具有相应条目的单个文件的签名。

### <a name="non-pnp-kernel-mode-boot-start-driver"></a><a href="" id="non-pnp-kernel-mode-boot-start-driver"></a> Boot-Start 驱动程序的非 PnP Kernel-Mode

若要符合 Windows Vista 和更高版本的 windows 版本的内核模式代码签名64策略，请将签名嵌入 *启动驱动程序* 文件中，如下所示：

1.  对[驱动程序文件进行测试签名](test-signing-a-driver-file.md)。

2.  [验证测试签名驱动程序文件的签名](verifying-the-signature-of-a-test-signed-driver-file.md)。

从 Windows Vista 开始，在 *启动启动驱动程序* 文件中嵌入签名对于32位版本的 Windows 是可选的。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入签名，但不需要嵌入签名。

[Pnp 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)不适用于非 PnP 驱动程序。

### <a name="pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a><a href="" id="pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> 不是 Boot-Start 驱动程序的 PnP Kernel-Mode 驱动程序

64位版本的 Windows Vista 和更高版本的 Windows 上的内核模式代码签名策略不需要非引导 PnP 驱动程序即可使用嵌入签名。 但是，如果驱动程序文件将包含嵌入的签名，则在对[驱动程序包的](driver-packages.md)[目录文件](catalog-files.md)进行签名之前，将签名嵌入驱动程序文件中。

对于不是 *启动启动驱动* 程序的 PnP 内核模式驱动程序，为驱动程序包签名目录文件符合 windows vista 和更高版本的64位版本上的内核模式代码签名策略，以及所有版本的 windows vista 和更高版本的 PnP 设备安装签名要求。

你可以提交请求，让 Windows 硬件质量实验室 (WHQL) 对编录文件进行测试签名。 或者，你可以使用测试证书自行对目录文件进行测试签名，如本部分中所述，用于对 PnP 内核模式 *启动驱动程序* 的编录文件进行测试签名。

### <a name="non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a><a href="" id="non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> 不是 Boot-Start 驱动程序的非 PnP Kernel-Mode 驱动程序

若要符合 Windows Vista 和更高版本的 windows Vista 和更高版本的内核模式代码签名64策略，请在驱动程序文件中嵌入签名或对[驱动程序包的](driver-packages.md)[目录文件](catalog-files.md)进行签名。

从 Windows Vista 开始，将签名嵌入驱动程序文件对于32位版本的 Windows 是可选的。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入签名，但不需要嵌入签名。

PnP 设备安装签名要求不适用于非 PnP 驱动程序。

**注意**   使用嵌入的签名通常比使用签名目录文件更简单、更有效。 有关使用嵌入的签名与签名的目录文件的优点和缺点的详细信息，请参阅对 [驱动程序进行测试签名](/windows-hardware/drivers)。

 

### <a name="to-embed-a-test-signature-in-a-file-for-a-non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a>在非 PnP 内核模式驱动程序的文件中嵌入测试签名，该驱动程序不是启动启动驱动程序

1.  对[驱动程序文件进行测试签名](test-signing-a-driver-file.md)。

2.  [验证测试签名驱动程序文件的签名](verifying-the-signature-of-a-test-signed-driver-file.md)。

### <a name="to-test-sign-a-catalog-file-for-a-non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a>为非 PnP 内核模式驱动程序（不是启动启动驱动程序）测试签名的目录文件

1.  [为非 PnP 驱动程序创建目录文件](creating-a-catalog-file-for-a-non-pnp-driver-package.md)。

2.  [对编录文件进行测试签名](test-signing-a-catalog-file.md)。

3.  [验证测试签名的目录文件的签名](verifying-the-signature-of-a-test-signed-catalog-file.md)。

 

