---
title: 在测试计算机上安装进行了测试签名的驱动程序包
description: 在测试计算机上安装进行了测试签名的驱动程序包
ms.assetid: d825acb6-d1de-4fc5-bde2-ea27bd706f61
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2692e4e6078731430dba343d441fb6401f9a4999
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383741"
---
# <a name="installing-a-test-signed-driver-package-on-the-test-computer"></a>在测试计算机上安装进行了测试签名的驱动程序包


你可以安装测试签名[驱动程序包](driver-packages.md)一次测试计算机上：

-   测试计算机已准备好安装测试签名的驱动程序或驱动程序包。 有关详细信息，请参阅[测试计算机配置为支持测试签名](configuring-the-test-computer-to-support-test-signing.md)。

-   测试证书复制到测试计算机上的受信任的根证书颁发机构证书存储中。 有关详细信息，请参阅[安装测试证书](installing-test-certificates.md)。

你可以安装测试签名[驱动程序包](driver-packages.md)通过在计算机上：

-   [DevCon](https://docs.microsoft.com/windows-hardware/drivers/devtest/devcon)工具，它是用于安装驱动程序的 WDK 命令行工具。

本主题将首先查看测试签名驱动程序包的过程，然后介绍如何在测试计算机上安装驱动程序包。 本主题使用*ToastPkg*示例驱动程序包。 在 WDK 安装目录中，包的源代码文件都位于*src\\常规\\toaster\\toastpkg*目录。

请按照以下步骤生成并测试登录*ToastPkg*示例驱动程序包：

1.  在签名的计算机上生成*ToastPkg*示例驱动程序包的内核模式二进制文件。 有关如何生成驱动程序的详细信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

2.  签名的计算机上创建*Contoso.com(Test)* 证书中所述[创建测试证书](creating-test-certificates.md)。

3.  签名的计算机上创建[编录文件](catalog-files.md)有关*ToastPkg*示例中所述的驱动程序包[测试签名的驱动程序包创建编录文件](creating-a-catalog-file-for-test-signing-a-driver-package.md)。

4.  签名在计算机上，测试登录*ToastPkg*示例驱动程序包的目录文件，如中所述[测试签名驱动程序包的目录文件](test-signing-a-driver-package-s-catalog-file.md)。 当驱动程序包时，使用*Contoso.com （测试）* 证书从*PrivateCertStor*e 表示测试签名。

5.  准备测试计算机以支持测试签名，如中所述[测试计算机配置为支持测试签名](configuring-the-test-computer-to-support-test-signing.md)。

6.  复制*Contoso.com(Test)* 证书到测试计算机上的受信任的根证书颁发机构证书存储中所述[安装测试证书](installing-test-certificates.md)。

下面的主题介绍如何*ToastPkg*示例驱动程序包可以安装在测试计算机上：

-   [使用 DevCon 工具安装驱动程序包](using-the-devcon-tool-to-install-a-driver-package.md)

一次[驱动程序包](driver-packages.md)是安装，可解决问题的测试签名的驱动程序加载中所述的方法通过[疑难解答安装和已签名的驱动程序包的负载问题](troubleshooting-install-and-load-problems-with-signed-driver-packages.md).

有关如何安装测试签名驱动程序包的详细信息，请参阅[Installing Test-Signed 驱动程序包](installing-test-signed-driver-packages.md)。

 

 





