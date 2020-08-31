---
title: 如何对驱动程序包进行发布签名
description: 如何对驱动程序包进行发布签名
ms.assetid: f02c0a50-01f1-456c-b432-c4d9e8cbc566
keywords:
- 版本签名驱动程序 WDK
- 驱动程序签名 WDK，发布签名包
- 对驱动程序进行签名 WDK，发布签名包
- 数字签名 WDK，版本签名驱动程序包
- 签名 WDK，版本签名驱动程序包
- 版本签名驱动程序 WDK
- 版本签名驱动程序 WDK，驱动程序包
- 版本签名驱动程序包 WDK
- 版本签名驱动程序包 WDK，关于测试签名驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 240522ea28c2382cc4275b96a6b69481b501ae96
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095265"
---
# <a name="how-to-release-sign-a-driver-package"></a>如何对驱动程序包进行发布签名


本部分提供对 [驱动程序包](driver-packages.md)进行发布签名时必须遵循的基本步骤。 这包括：

-   从商业证书颁发机构 (CA) 获取 [软件发行者证书 (SPC) ](software-publisher-certificate.md) 。

-   为发布签名准备 [驱动程序包](driver-packages.md) 。 这包括创建包含驱动程序包数字签名的 [目录文件](catalog-files.md)。

-   对驱动程序包的目录文件进行发布签名。

-   通过嵌入签名对驱动程序进行发布签名。 如果驱动程序是 *启动启动驱动*程序，则必须在驱动程序中嵌入数字签名。

本节中的每个主题都介绍了发布签名过程中的一个单独过程，并提供了有关该过程的相关一般信息。 此外，每个主题都指向提供有关过程的详细信息的其他主题。

**注意**   本部分讨论驱动程序发行者必须手动对驱动程序包进行发布签名时所涉及的步骤。 [硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?linkid=227016)包含各种设备类型的[测试类别](https://go.microsoft.com/fwlink/p/?linkid=189178)。 如果此列表中包含设备类型的测试类别，则驱动程序发行者应为驱动程序包获取 [WHQL 版本签名](whql-release-signature.md) ，而不是手动对驱动程序包进行发布签名。

 

在此部分中，单独的计算机用于对驱动程序进行发布签名所涉及的各种进程。 这些计算机的引用如下所示：

<a href="" id="--------signing-computer"></a>正在为 **计算机签名**  
这是用于对 Windows Vista 和更高版本的 Windows 的驱动程序包进行发布签名的计算机。 此计算机必须运行 Windows XP SP2 或更高版本的 Windows。 若要使用 [驱动程序签名工具](../devtest/tools-for-signing-drivers.md)，此计算机必须安装 windows Vista 及更高版本的 Windows 驱动程序工具包 (WDK) 。

<a href="" id="test-computer"></a>**测试计算机**  
此计算机用于安装和测试发布签名的驱动程序包。 此计算机必须运行 Windows Vista 或更高版本的 Windows。

在讨论版本签名过程时，本节中的主题使用 *toastpkg.inf* 示例驱动程序包。 在 WDK 安装目录中， *toastpkg.inf* 驱动程序包位于 *src \\ general \\ toaster \\ toastpkg.inf* 目录中。

本节包含下列主题：

[获取软件发行者证书 (SPC)](obtaining-a-software-publisher-certificate--spc-.md)

[创建用于对驱动程序包进行发布签名的目录文件](creating-a-catalog-file-for-release-signing-a-driver-package.md)

[对驱动程序包的目录文件进行发布签名](release-signing-a-driver-package-s-catalog-file.md)

[通过嵌入签名对驱动程序进行发布签名](release-signing-a-driver-through-an-embedded-signature.md)

[验证发布签名](verifying-the-release-signature.md)

[配置支持发布签名的计算机](configuring-a-computer-to-support-release-signing.md)

[安装进行了发布签名的驱动程序包](installing-a-release-signed-driver-package.md)

 

