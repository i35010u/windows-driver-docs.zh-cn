---
title: 对驱动程序包进行发布签名
description: 对驱动程序包进行发布签名
ms.assetid: 57125c3b-55f0-4b60-b4d9-1408e26faccb
keywords:
- 驱动程序签名 WDK、 驱动程序包
- 签署驱动程序 WDK、 驱动程序包
- 数字签名 WDK、 驱动程序包
- WDK、 驱动程序包签名
- CAT 文件
- .cat 文件
- 目录文件 WDK 驱动程序签名，签名版本
- 公开发布的版本驱动程序签名 WDK，有关对版本进行签名
- 发布有关版本签名签名 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da5af0cfc1d32625baa6a14654a209fbde2ba8c1
ms.sourcegitcommit: a678a339f09fbd56a3a6124c0fe86194fedb2ed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57560614"
---
# <a name="release-signing-driver-packages"></a>对驱动程序包进行发布签名


在本部分中，对在 Windows Vista 和更高版本的 Windows 驱动程序进行签名的计算机被称为*签名计算机*。 签名的计算机必须运行 Windows XP SP2 或更高版本的 Windows 操作系统。 例如，适用于 Windows 7 上的发布的驱动程序可以运行的 Windows Vista 的计算机上进行签名。

此外，签名的计算机必须具有[驱动程序签名工具](https://msdn.microsoft.com/library/windows/hardware/ff552958)安装。

**请注意**  必须使用的新版[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778) Windows Vista 和更高版本的 Windows Driver Kit (WDK) 中提供的工具。 此工具的早期版本不支持内核模式代码签名策略适用于 Windows Vista 和更高版本的 Windows。

 

若要符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)并[插即用 (PnP) 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)的 Windows Vista 和更高版本的 Windows 中，登录用于作为版本的驱动程序如下所示，驱动程序的类型。

**请注意**   Windows 代码签名策略要求的已签名[编录文件](catalog-files.md)驱动程序会安装在系统组件和驱动程序数据库中。 即插即用设备安装会自动安装驱动程序数据库中的即插即用驱动程序的目录文件。 但是，如果使用签名的编录文件进行签名的非 PnP 驱动程序，将安装驱动程序的安装应用程序还必须安装目录文件驱动程序数据库中。

 

### <a href="" id="pnp-kernel-mode-boot-start-driver"></a> PnP Kernel-Mode Boot-Start Driver

若要符合内核模式代码签名策略文件，如下所示：

1.  [发布符号的驱动程序文件](release-signing-a-driver-file.md)与[软件发布者证书 (SPC)](software-publisher-certificate.md)。

2.  [验证驱动程序文件的 SPC 签名](verifying-the-signature-of-a-release-signed-driver-file.md)。

从 Windows Vista，嵌入在签名开始*引导启动驱动程序*文件是可选的 32 位版本的 Windows。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入式的签名，则不需要的嵌入式的签名。

若要符合[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)的 Windows Vista 和更高版本的 Windows 中，你必须获取一个已签名[编录文件](catalog-files.md)或签署的编录文件[驱动程序包](driver-packages.md)。 如果驱动程序文件还将包括的嵌入式的签名，签名文件中嵌入驱动程序之前对驱动程序包的目录文件进行签名。

如果[硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)具有测试程序驱动程序中，获取[WHQL 版本签名](whql-release-signature.md)驱动程序包。 如果 HCK 不具有该驱动程序，测试程序[创建编录文件](creating-a-catalog-file-for-a-pnp-driver-package.md)并登录[编录文件](catalog-files.md)，如下所示：

**签名 64 位版本的目录文件**

你可以签署编录文件的 64 位操作系统，如下所示：

1.  [签署编录文件与 SPC](signing-a-catalog-file-with-an-spc.md)用于驱动程序文件中嵌入签名。

2.  [验证目录文件的 SPC 签名](verifying-the-spc-signature-of-a-catalog-file.md)。 你可以验证目录文件的签名或可以验证签名的编录文件中的单个文件条目。

**签名目录文件以 32 位版本**

你可以注册[编录文件](catalog-files.md)与一个 SPC，对于 64 位版本，或使用的部分中所述[商业版本发布证书](commercial-release-certificate.md)，如下所示：

1.  [使用商业版本发布证书目录文件进行签名](signing-a-catalog-file-with-a-commercial-release-certificate.md)。

2.  [验证目录文件的签名](verifying-the-signature-of-a-catalog-file-signed-by-a-commercial-relea.md)。 你可以验证目录文件的签名或可以验证签名的编录文件中的单个文件条目。

### <a href="" id="non-pnp-kernel-mode-boot-start-driver"></a> 非 PnP 内核模式引导启动驱动程序

若要符合内核模式代码签名的 64 位版本的 Windows Vista 和更高版本的 Windows 的策略，将嵌入在签名*引导启动驱动程序*文件，如下所示：

1.  [发布符号的驱动程序文件](release-signing-a-driver-file.md)与一个 SPC。

2.  [验证驱动程序文件的 SPC 签名](verifying-the-signature-of-a-release-signed-driver-file.md)。

从 Windows Vista，嵌入在签名开始*引导启动驱动程序*文件是可选的 32 位版本的 Windows。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入式的签名，则不需要的嵌入式的签名。

即插即用设备安装签名要求不适用于非 PnP 驱动程序。

### <a href="" id="pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> 即插即用的内核模式驱动程序，它不是一个引导启动驱动程序

内核模式代码签名 64 位版本的 Windows Vista 和更高版本的 Windows 上的策略不需要非启动即插即用驱动程序具有嵌入式的签名。 但是，如果驱动程序文件中包含的嵌入式的签名，签名驱动程序在文件中嵌入签名前[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)。

若要符合即插即用设备安装签名要求，你必须获取签名的编录文件或驱动程序包的目录文件进行签名。

如果硬件认证工具包 (HCK)。

### <a href="" id="non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> 非 PnP 内核模式驱动程序，它不是一个引导启动驱动程序

若要符合内核模式代码签名策略的 64 位版本 Windows Vista 和更高版本的 Windows，驱动程序文件中嵌入签名或签名的编录文件[驱动程序包](driver-packages.md)。

从 Windows Vista 开始，在驱动程序文件中嵌入签名是可选的 32 位版本的 Windows。 尽管 Windows 将检查内核模式驱动程序文件是否具有嵌入式的签名，则不需要的嵌入式的签名。

即插即用设备安装签名要求不适用于非 PnP 驱动程序。

**请注意**  使用嵌入式的签名是通常更为简单且更高效比使用签名的编录文件。 有关使用嵌入式的签名与签名的编录文件的优缺点的详细信息，请参阅[测试签名驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/signing-a-driver)。

 

若要在非 PnP 内核模式驱动程序不是文件中嵌入版本签名*引导启动驱动程序*，请执行以下步骤：

1.  [驱动程序文件进行签名](release-signing-a-driver-file.md)与一个 SPC。

2.  [验证驱动程序文件的签名](verifying-the-signature-of-a-release-signed-driver-file.md)。

对版本签名目录文件非 PnP 内核模式驱动程序不是*引导启动驱动程序*，请执行以下步骤：

1.  [创建非 PnP 驱动程序的目录文件](creating-a-catalog-file-for-a-non-pnp-driver-package.md)。

2.  [签署编录文件与一个 SPC](signing-a-catalog-file-with-an-spc.md)。

3.  [验证目录文件的 SPC 签名](verifying-the-spc-signature-of-a-catalog-file.md)。

如果此类型的驱动程序都有一个已签名[编录文件](catalog-files.md)安装驱动程序的安装应用程序必须在系统组件和驱动程序数据库中的编录文件安装而不是嵌入式签名。 有关详细信息，请参阅[为非 PnP 驱动程序安装 Release-Signed 目录文件](installing-a-release-signed-catalog-file-for-a-non-pnp-driver.md)。

 

 





