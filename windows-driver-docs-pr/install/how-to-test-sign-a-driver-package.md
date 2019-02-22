---
title: 如何测试签名驱动程序包
description: 如何测试签名驱动程序包
ms.assetid: 992f0974-0b0e-4c96-ad16-c5894067896c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b93c83d44aa25ac15fef1a4beaa4264aaa80891a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524136"
---
# <a name="how-to-test-sign-a-driver-package"></a>如何测试签名驱动程序包


本部分提供有关的基本步骤的信息，则必须按照时您测试签名[驱动程序包](driver-packages.md)。 

测试签名是指使用测试证书进行签名的预发布版本[驱动程序包](driver-packages.md)以用于测试计算机。 具体而言，这允许开发人员使用自签名的证书，例如签名内核模式二进制文件[ **MakeCert** ](https://msdn.microsoft.com/library/windows/hardware/ff548309)工具生成。 此功能允许开发人员要进行测试驱动程序签名验证已启用内核模式在 Windows 上的二进制文件。

Windows 支持仅用于开发和测试目的测试签名的驱动程序。 测试签名的驱动程序不得用于生产目的或发布给客户。

本部分包括主题，描述了这些步骤，并提供示例，如下所示：

-   创建测试证书用于签署驱动程序包。 在本部分中的步骤进行了介绍创建和使用一个名为的自签名的测试证书*Contoso.com(Test)*。 在此部分中讨论的许多示例中使用此证书。

-   正在准备[驱动程序包](driver-packages.md)进行测试签名。 这包括创建[编录文件](catalog-files.md)，其中包含的数字签名。

-   测试签名驱动程序包的目录文件通过使用*Contoso.com(Test)* 证书。

-   测试签名通过嵌入式签名的驱动程序通过使用*Contoso.com(Test)* 证书。

    **请注意**  具有将嵌入在驱动程序中的数字签名，如果驱动程序*引导启动驱动程序*。

     

在本部分中的每个主题介绍在测试签名过程中，另一个过程，并提供您需要了解该过程的一般信息。 此外，每个主题会转到其他主题提供有关该过程的详细的信息。

在本部分中，不同的计算机用于测试签名驱动程序所涉及的各种流程。 这些计算机称为，如下所示：

<a href="" id="signing-computer"></a>**签名的计算机**  
这是用于测试签名驱动程序包适用于 Windows Vista 和更高版本的 Windows 的计算机。 此计算机必须运行 Windows XP SP2 或更高版本的 Windows。 若要使用[驱动程序签名工具](https://msdn.microsoft.com/library/windows/hardware/ff552958)、 此计算机必须安装 Windows Vista 和更高版本的 Windows Driver Kit (WDK) 安装。

<a href="" id="test-computer"></a>**测试计算机**  
这是用于安装和测试的测试签名驱动程序包的计算机。 此计算机必须运行 Windows Vista 或更高版本的 Windows。

此主题部分使用*ToastPkg*引入测试签名过程的示例驱动程序包。 在 WDK 安装目录中， *ToastPkg*驱动程序包位于*src\\常规\\toaster\\toastpkg*目录。

**请注意**  WDK 包含一个示例命令脚本，演示到正确的测试签名的分步过程*ToastPkg*示例[驱动程序包](driver-packages.md)。 您可以修改此脚本保存到测试签名驱动程序包。 在 WDK 安装目录中，该示例位于*src\\常规\\构建\\driversigning\\selfsign_example.cmd*。 关于测试签名的其他说明所述*src\\常规\\构建\\driversigning\\selfsign_readme.htm*。

 

本部分包括以下主题：

[创建测试证书](creating-test-certificates.md)

[查看测试证书](viewing-test-certificates.md)

[为测试签名驱动程序包创建编录文件](creating-a-catalog-file-for-test-signing-a-driver-package.md)

[测试签名驱动程序包的目录文件](test-signing-a-driver-package-s-catalog-file.md)

[测试签名通过嵌入式签名的驱动程序](test-signing-a-driver-through-an-embedded-signature.md)

[配置测试计算机以支持测试签名](configuring-the-test-computer-to-support-test-signing.md)

[安装测试证书](installing-test-certificates.md)

[验证测试签名](verifying-the-test-signature.md)

[在测试计算机上安装测试签名驱动程序包](installing-a-test-signed-driver-package-on-the-test-computer.md)

 

 





