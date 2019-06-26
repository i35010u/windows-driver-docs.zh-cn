---
title: 对驱动程序包进行测试签名
description: 对驱动程序包进行测试签名
ms.assetid: 84727762-5ba0-48ea-8d5a-7ac54aadbb7e
keywords:
- 驱动程序签名 WDK、 驱动程序包
- 签署驱动程序 WDK、 驱动程序包
- 数字签名 WDK、 驱动程序包
- WDK、 驱动程序包签名
- 驱动程序数据包数字签名 WDK
- 数据包数字签名 WDK
- 测试签名驱动程序 WDK、 驱动程序包
- 测试签名驱动程序包 WDK
- 测试签名驱动程序包 WDK，有关测试签名驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3774b4f68596745731e02b857f04f6fec270a059
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380971"
---
# <a name="test-signing-driver-packages"></a>对驱动程序包进行测试签名


在本部分中，在 Windows Vista 和更高版本的 Windows 发行测试签名的驱动程序的计算机被称为*签名计算机*。 签名的计算机必须运行 Windows XP SP2 或更高版本的 Windows。 例如，适用于 Windows 7 上的发布的驱动程序可以运行 Windows Vista 的计算机上进行签名。

若要使用[驱动程序签名工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-signing-drivers)、 签名的计算机必须具有 Windows Vista 和更高版本的 WDK 安装。

**请注意**  必须使用的新版[ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool) Windows Vista 和更高版本的 Windows Driver Kit (WDK) 中提供的工具。 SignTool 的早期版本不支持内核模式代码签名策略适用于 Windows Vista 和更高版本的 Windows。

 

若要符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)并[插即用 (PnP) 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)的 Windows Vista 和更高版本的 Windows 中，你必须登录期间的驱动程序开发和测试该驱动程序。 你可以登录签名的计算机上的驱动程序，如下所示，基于驱动程序类型。

**请注意**   Windows 代码签名策略要求已签名[编录文件](catalog-files.md)有关[驱动程序包](driver-packages.md)安装在系统组件和驱动程序数据库中。 即插即用设备安装会自动安装驱动程序数据库中的即插即用驱动程序的目录文件。 但是，如果使用签名的编录文件进行签名的非 PnP 驱动程序，将安装驱动程序的安装应用程序还必须安装目录文件驱动程序数据库中。

 

### <a href="" id="pnp-kernel-mode-boot-start-driver"></a> PnP Kernel-Mode Boot-Start Driver

若要符合内核模式代码签名策略文件，如下所示：

1.  [测试签名的驱动程序文件](test-signing-a-driver-file.md)。

2.  [验证测试签名驱动程序文件的签名](verifying-the-signature-of-a-test-signed-driver-file.md)。

从 Windows Vista，嵌入在签名开始*引导启动驱动程序*文件是可选的 32 位版本的 Windows。 尽管 Windows 将检查内核模式驱动程序文件是否包含嵌入式的签名，则不需要的嵌入式的签名。

若要符合[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)的 Windows Vista 和更高版本的 Windows 中，您必须测试签名[编录文件](catalog-files.md)为[驱动程序包](driver-packages.md). 如果驱动程序文件还将包括的嵌入式的签名，签名文件中嵌入驱动程序之前对驱动程序包的目录文件进行签名。

您可以提交申请，将[Windows 硬件质量实验室 (WHQL) 测试签名](whql-test-signature-program.md)[编录文件](catalog-files.md)。 或者，你可以测试签名目录文件自己带有测试证书，如下所示：

1.  [创建编录文件](creating-a-catalog-file-for-a-test-signed-driver-package.md)。

2.  [测试签名的编录文件](test-signing-a-catalog-file.md)。

3.  [验证测试签名的目录文件的签名](verifying-the-signature-of-a-test-signed-catalog-file.md)。

    你可以验证目录文件本身的签名或签名的编录文件中具有相应的项的单个文件。

### <a href="" id="non-pnp-kernel-mode-boot-start-driver"></a> 非 PnP 内核模式引导启动驱动程序

若要符合内核模式代码签名的 64 位版本的 Windows Vista 和更高版本的 Windows 的策略，将嵌入在签名*引导启动驱动程序*文件，如下所示：

1.  [测试签名的驱动程序文件](test-signing-a-driver-file.md)。

2.  [验证测试签名驱动程序文件的签名](verifying-the-signature-of-a-test-signed-driver-file.md)。

从 Windows Vista，嵌入在签名开始*引导启动驱动程序*文件是可选的 32 位版本的 Windows。 尽管 Windows 将检查内核模式驱动程序文件是否包含嵌入式的签名，则不需要的嵌入式的签名。

[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)不适用于非 PnP 驱动程序。

### <a href="" id="pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> 即插即用的内核模式驱动程序，它不是一个引导启动驱动程序

内核模式代码签名 64 位版本的 Windows Vista 和更高版本的 Windows 上的策略不需要非启动即插即用驱动程序具有嵌入式的签名。 但是，如果驱动程序文件中包含的嵌入式的签名，签名驱动程序在文件中嵌入签名前[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)。

即插即用的内核模式驱动程序不是*引导启动驱动程序*，对目录文件进行签名的驱动程序包符合内核模式代码签名上 64 位版本的 Windows Vista 和更高版本的 Windows，以及策略与即插即用设备安装签名所有版本的 Windows Vista 及更高版本的要求。

您可以提交申请，将 Windows 硬件质量实验室 (WHQL) 测试签名。

### <a href="" id="non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> 非 PnP 内核模式驱动程序，它不是一个引导启动驱动程序

若要符合内核模式代码签名的 64 位版本的 Windows Vista 和更高版本的 Windows 的策略，在登录的驱动程序文件中嵌入签名[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)。

从 Windows Vista 开始，在驱动程序文件中嵌入签名是可选的 32 位版本的 Windows。 尽管 Windows 将检查内核模式驱动程序文件是否包含嵌入式的签名，则不需要的嵌入式的签名。

即插即用设备安装签名要求不适用于非 PnP 驱动程序。

**请注意**  使用嵌入式的签名是通常更为简单且更高效比使用签名的编录文件。 有关使用嵌入式的签名与签名的编录文件的优缺点的详细信息，请参阅[测试签名驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

 

### <a name="to-embed-a-test-signature-in-a-file-for-a-non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a>若要在不是一个引导启动驱动程序的非 PnP 内核模式驱动程序的文件中嵌入测试签名

1.  [测试签名的驱动程序文件](test-signing-a-driver-file.md)。

2.  [验证测试签名驱动程序文件的签名](verifying-the-signature-of-a-test-signed-driver-file.md)。

### <a name="to-test-sign-a-catalog-file-for-a-non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a>对测试签名目录文件以非 PnP 内核模式驱动程序的不是引导启动驱动程序

1.  [创建非 PnP 驱动程序的目录文件](creating-a-catalog-file-for-a-non-pnp-driver-package.md)。

2.  [测试签名的编录文件](test-signing-a-catalog-file.md)。

3.  [验证测试签名的目录文件的签名](verifying-the-signature-of-a-test-signed-catalog-file.md)。

 

 





