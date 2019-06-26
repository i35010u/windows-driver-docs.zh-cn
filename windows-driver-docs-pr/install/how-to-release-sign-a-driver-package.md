---
title: 如何对驱动程序包进行发布签名
description: 如何对驱动程序包进行发布签名
ms.assetid: f02c0a50-01f1-456c-b432-c4d9e8cbc566
keywords:
- 版本签名驱动程序 WDK
- 驱动程序签名 WDK，版本签名包
- 签署驱动程序 WDK，版本签名包
- 数字签名 WDK，版本签名驱动程序包
- WDK，版本签名驱动程序包签名
- 版本签名驱动程序 WDK
- 版本签名驱动程序 WDK、 驱动程序包
- WDK 版本签名驱动程序包
- 版本签名驱动程序包 WDK，有关测试签名驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 011887145b17c78b44d96717ddff238c2d8ec056
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387036"
---
# <a name="how-to-release-sign-a-driver-package"></a>如何对驱动程序包进行发布签名


本部分提供的基本步骤，则必须按照当您发布符号[驱动程序包](driver-packages.md)。 这包括以下内容：

-   获取[软件发布者证书 (SPC)](software-publisher-certificate.md)从商业证书颁发机构 (CA)。

-   正在准备[驱动程序包](driver-packages.md)版本签名。 这包括创建[编录文件](catalog-files.md)，其中包含驱动程序包的数字签名。

-   版本签名驱动程序包的目录文件。

-   通过嵌入签名的驱动程序版本签名。 您必须嵌入在驱动程序中的数字签名，如果驱动程序*引导启动驱动程序*。

在本部分中的每个主题描述在版本签名过程中，另一个过程，并提供你需要了解有关该过程的一般信息。 此外，每个主题会转到其他主题提供有关该过程的详细的信息。

**请注意**  驱动程序发布服务器具有对手动发布签名的驱动程序包时，本部分讨论所涉及的步骤。 [硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)已[测试类别](https://go.microsoft.com/fwlink/p/?linkid=189178)多种设备类型。 如果此列表中包含的设备类型的测试类别，应获取驱动程序发行者[WHQL 版本签名](whql-release-signature.md)驱动程序包，而不是手动版本的驱动程序对程序包进行签名。

 

在本部分中，不同的计算机用于版本签名驱动程序所涉及的各种流程。 这些计算机称为，如下所示：

<a href="" id="--------signing-computer"></a> **签名的计算机**  
这是使用版本签名驱动程序包适用于 Windows Vista 和更高版本的 Windows 的计算机。 此计算机必须运行 Windows XP SP2 或更高版本的 Windows。 若要使用[驱动程序签名工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-signing-drivers)、 此计算机必须安装 Windows Vista 和更高版本的 Windows Driver Kit (WDK) 安装。

<a href="" id="test-computer"></a>**测试计算机**  
这是用于安装和测试已发布签名驱动程序包的计算机。 此计算机必须运行 Windows Vista 或更高版本的 Windows。

此主题讨论版本签名进程，部分使用*ToastPkg*示例驱动程序包。 在 WDK 安装目录中， *ToastPkg*驱动程序包位于*src\\常规\\toaster\\toastpkg*目录。

本部分包含以下主题：

[获取软件发布者证书 (SPC)](obtaining-a-software-publisher-certificate--spc-.md)

[为版本签名的驱动程序包创建编录文件](creating-a-catalog-file-for-release-signing-a-driver-package.md)

[版本签名驱动程序包的目录文件](release-signing-a-driver-package-s-catalog-file.md)

[通过嵌入签名的驱动程序签名版本](release-signing-a-driver-through-an-embedded-signature.md)

[验证版本签名](verifying-the-release-signature.md)

[配置计算机以支持发布签名](configuring-a-computer-to-support-release-signing.md)

[安装已发布签名驱动程序包](installing-a-release-signed-driver-package.md)

 

 





