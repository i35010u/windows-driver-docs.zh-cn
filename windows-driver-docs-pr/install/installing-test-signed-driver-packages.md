---
title: 安装已进行测试签名的驱动程序包
description: 安装已进行测试签名的驱动程序包
keywords:
- 测试签名驱动程序 WDK，安装测试签名的驱动程序包
- 驱动程序签名 WDK，驱动程序包
- 对驱动程序进行签名 WDK，驱动程序包
- 数字签名 WDK，驱动程序包
- 签名 WDK，驱动程序包
- 驱动程序包数字签名 WDK
- 包数字签名 WDK
- 测试签名驱动程序 WDK，驱动程序包
- 安装测试签名驱动程序包 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39605df96d7fb62c6e819522f0bbdbae5b52a204
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823086"
---
# <a name="installing-test-signed-driver-packages"></a>安装已进行测试签名的驱动程序包


从 Windows Vista 开始，如果满足以下条件，则测试签名的 [驱动程序包](driver-packages.md) 应在无需用户交互的情况下进行安装和加载：

-   驱动程序包符合 Windows Vista 和更高版本的 Windows 的一般要求。

-   驱动程序包已签名，并验证签名，如 [测试签名驱动程序包](test-signing-driver-packages.md)中所述。

-   驱动程序包在签名后不会更改。

-   在测试计算机上正确安装了用于对驱动程序包进行签名的测试证书，如在 [测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)中所述。

-   如果非 PnP 驱动程序具有已签名的 [目录文件](catalog-files.md) 而不是嵌入的签名，则安装该驱动程序的安装应用程序已将目录文件安装在系统目录根目录中，如 [安装非 PnP 驱动程序的 Test-Signed 目录文件](installing-a-test-signed-catalog-file-for-a-non-pnp-driver.md)中所述。

-   在测试计算机上启用测试签名。 有关详细信息，请参阅 [TESTSIGNING Boot Configuration 选项](the-testsigning-boot-configuration-option.md)。

有关如何安装测试签名驱动程序包的概述，请参阅 [在测试计算机上安装 Test-Signed 驱动程序包](installing-a-test-signed-driver-package-on-the-test-computer.md)。

有关如何解决安装问题的详细信息，请参阅 [排查签名驱动程序包的安装和加载问题](./detecting-driver-load-errors.md)。

 

