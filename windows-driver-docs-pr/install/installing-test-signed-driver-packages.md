---
title: 安装测试签名驱动程序包
description: 安装测试签名驱动程序包
ms.assetid: 6abbe51c-0fdf-465f-b1f2-d48e593a4f0e
keywords:
- 测试签名驱动程序 WDK，安装测试签名驱动程序包
- 驱动程序签名 WDK、 驱动程序包
- 签署驱动程序 WDK、 驱动程序包
- 数字签名 WDK、 驱动程序包
- WDK、 驱动程序包签名
- 驱动程序数据包数字签名 WDK
- 数据包数字签名 WDK
- 测试签名驱动程序 WDK、 驱动程序包
- 安装测试签名的驱动程序包 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec819f268b48609a7d1529d033da5857f1d06349
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533581"
---
# <a name="installing-test-signed-driver-packages"></a>安装测试签名驱动程序包


从 Windows Vista，测试签名开始[驱动程序包](driver-packages.md)应安装并加载无需用户交互，如果满足以下条件：

-   驱动程序包符合通用要求的 Windows Vista 和更高版本的 Windows。

-   驱动程序包进行签名和验证签名，如中所述[测试签名驱动程序包](test-signing-driver-packages.md)。

-   驱动程序包不会更改后对其进行签名。

-   已用于签署驱动程序包的测试证书正确安装的测试计算机上，如中所述[测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。

-   如果非 PnP 驱动程序包含一个已签名[编录文件](catalog-files.md)而不是嵌入式签名，将安装驱动程序的安装应用程序已安装的编录文件系统目录根目录中中所述[安装适用于非 PnP 驱动程序测试签名目录文件](installing-a-test-signed-catalog-file-for-a-non-pnp-driver.md)。

-   在测试计算机上启用测试签名。 有关详细信息，请参阅[TESTSIGNING 启动配置选项](the-testsigning-boot-configuration-option.md)。

有关如何安装测试签名驱动程序包的概述，请参阅[测试计算机上安装 Test-Signed 驱动程序包](installing-a-test-signed-driver-package-on-the-test-computer.md)。

有关如何解决安装问题的详细信息，请参阅[疑难解答安装和已签名的驱动程序包的负载问题](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)。

 

 





