---
title: 在测试计算机上安装进行了测试签名的驱动程序包
description: 在测试计算机上安装进行了测试签名的驱动程序包
ms.assetid: d825acb6-d1de-4fc5-bde2-ea27bd706f61
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf4d1633ebd7887c4d69d9276fcf0fa1c39a370
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097275"
---
# <a name="installing-a-test-signed-driver-package-on-the-test-computer"></a>在测试计算机上安装进行了测试签名的驱动程序包


您可以在测试计算机上安装一次测试签名的 [驱动程序包](driver-packages.md) ：

-   测试计算机已准备好安装测试签名的驱动程序或驱动程序包。 有关详细信息，请参阅 [配置测试计算机以支持测试签名](configuring-the-test-computer-to-support-test-signing.md)。

-   测试证书将复制到测试计算机上的 "受信任的根证书颁发机构" 证书存储中。 有关详细信息，请参阅 [安装测试证书](installing-test-certificates.md)。

可以通过以下步骤在计算机上安装测试签名的 [驱动程序包](driver-packages.md) ：

-   [DevCon](../devtest/devcon.md)工具，它是用于安装驱动程序的 WDK 命令行工具。

本主题将首先查看对驱动程序包进行测试签名的过程，然后说明如何在测试计算机上安装驱动程序包。 本主题使用 *toastpkg.inf* 示例驱动程序包。 在 WDK 安装目录中，包的源文件位于 *src \\ general \\ toaster \\ toastpkg.inf* 目录中。

按照以下步骤生成和测试 *toastpkg.inf* 示例驱动程序包的签名：

1.  在签名计算机上，生成 *toastpkg.inf* 示例驱动程序包的内核模式二进制文件。 有关如何生成驱动程序的详细信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

2.  在签名计算机上，创建 *Contoso.com (测试) * 证书，如 [创建测试证书](creating-test-certificates.md)中所述。

3.  在签名计算机上，根据[创建用于对驱动程序包进行测试签名的目录文件](creating-a-catalog-file-for-test-signing-a-driver-package.md)中所述，为*toastpkg.inf*示例驱动程序包创建[编录文件](catalog-files.md)。

4.  在签名计算机上，对 *toastpkg.inf* 示例驱动程序包的目录文件进行测试签名，如对 [驱动程序包的目录文件进行测试签名](test-signing-a-driver-package-s-catalog-file.md)中所述。 对驱动程序包进行签名时，使用 *Contoso.com () 测试 * *PrivateCertStor*e 中的测试签名证书。

5.  准备测试计算机以支持测试签名，如将 [测试计算机配置为支持测试签名](configuring-the-test-computer-to-support-test-signing.md)中所述。

6.  如[安装测试证书](installing-test-certificates.md)中所述，将*Contoso.com (测试) *证书复制到测试计算机上受信任的根证书颁发机构证书存储。

以下主题介绍了如何在测试计算机上安装 *toastpkg.inf* 示例驱动程序包：

-   [使用 DevCon 工具安装驱动程序包](using-the-devcon-tool-to-install-a-driver-package.md)

安装 [驱动程序包](driver-packages.md) 后，您可以通过 [使用已签名的驱动程序包的安装和加载问题疑难解答](./detecting-driver-load-errors.md)中所述的方法，对加载测试签名驱动程序的问题进行故障排除。

有关如何安装测试签名驱动程序包的详细信息，请参阅 [安装测试签名的驱动](installing-test-signed-driver-packages.md)程序包。

 

