---
title: 如何对驱动程序包进行测试签名
description: 如何对驱动程序包进行测试签名
ms.assetid: 992f0974-0b0e-4c96-ad16-c5894067896c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 370242ed2976478394474f4183b97841755a5c7b
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095247"
---
# <a name="how-to-test-sign-a-driver-package"></a>如何对驱动程序包进行测试签名


本部分提供有关测试 [驱动程序包](driver-packages.md)时必须遵循的基本步骤的信息。 

测试签名是指使用测试证书对要在测试计算机上使用的 [驱动程序包](driver-packages.md) 的预发布版本进行签名。 具体而言，这允许开发人员使用自签名证书（如 [**MakeCert**](../devtest/makecert.md) 工具生成的证书）对内核模式二进制文件进行签名。 此功能使开发人员能够在启用了驱动程序签名验证的 Windows 上测试内核模式的二进制文件。

Windows 只支持用于开发和测试目的的测试签名驱动程序。 测试签名的驱动程序不得用于生产目的或发布给客户。

本部分包含的主题介绍了这些步骤，并提供了示例，如下所示：

-   创建用于签署驱动程序包的测试证书。 本部分介绍如何创建并使用名为 Contoso.com 的自签名测试证书 * (测试) *。 此证书用于此部分中讨论的许多示例。

-   正在为测试签名准备 [驱动程序包](driver-packages.md) 。 这包括创建包含数字签名的 [目录文件](catalog-files.md) 。

-   使用 *Contoso.com (测试) * 证书对驱动程序包的目录文件进行测试签名。

-   通过嵌入签名对驱动程序进行测试签名，方法是使用 *Contoso.com (测试) * 证书。

    **注意**   如果驱动程序是*启动启动驱动*程序，则必须在驱动程序中嵌入数字签名。

     

本节中的每个主题都介绍了测试签名过程中的一个单独过程，并提供了了解该过程所需的一般信息。 此外，每个主题都指向提供有关过程的详细信息的其他主题。

在此部分中，单独的计算机用于对驱动程序进行测试签名所涉及的各种进程。 这些计算机的引用如下所示：

<a href="" id="signing-computer"></a>**正在为计算机签名**  
此计算机用于对 Windows Vista 和更高版本的 Windows 的驱动程序包进行测试签名。 此计算机必须运行 Windows XP SP2 或更高版本的 Windows。 为了使用 [驱动程序签名工具](../devtest/tools-for-signing-drivers.md)，此计算机必须安装 windows Vista 和更高版本的 Windows 驱动程序工具包 (WDK) 。

<a href="" id="test-computer"></a>**测试计算机**  
此计算机用于安装和测试测试签名的驱动程序包。 此计算机必须运行 Windows Vista 或更高版本的 Windows。

本节中的主题使用 *toastpkg.inf* 示例驱动程序包来引入测试签名过程。 在 WDK 安装目录中， *toastpkg.inf* 驱动程序包位于 *src \\ general \\ toaster \\ toastpkg.inf* 目录中。

**注意**   WDK 包含一个示例命令脚本，其中显示了对*toastpkg.inf*示例[驱动程序包](driver-packages.md)进行正确测试的分步过程。 您可以修改此脚本以对您自己的驱动程序包进行测试签名。 在 WDK 安装目录中，该示例位于 *src \\ general \\ build \\ driversigning \\ selfsign_example .cmd*中。 *Src \\ general \\ build \\ driversigning \\selfsign_readme.htm*中介绍了有关测试签名的其他说明。

 

本节包括下列主题：

[创建测试证书](creating-test-certificates.md)

[查看测试证书](viewing-test-certificates.md)

[创建用于对驱动程序包进行测试签名的目录文件](creating-a-catalog-file-for-test-signing-a-driver-package.md)

[对驱动程序包的目录文件进行测试签名](test-signing-a-driver-package-s-catalog-file.md)

[通过嵌入式签名对驱动程序进行测试签名](test-signing-a-driver-through-an-embedded-signature.md)

[配置支持测试签名的测试计算机](configuring-the-test-computer-to-support-test-signing.md)

[安装测试证书](installing-test-certificates.md)

[验证测试签名](verifying-the-test-signature.md)

[在测试计算机上安装进行了测试签名的驱动程序包](installing-a-test-signed-driver-package-on-the-test-computer.md)

 

