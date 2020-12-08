---
title: 创建用于对驱动程序包进行测试签名的目录文件
description: 创建用于对驱动程序包进行测试签名的目录文件
keywords:
- 测试签名驱动程序包 WDK，编录文件
- 目录文件 WDK 驱动程序签名，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 785d86f9d973f65a58c9d02403d18c0cbae01d65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827827"
---
# <a name="creating-a-catalog-file-for-test-signing-a-driver-package"></a>创建用于对驱动程序包进行测试签名的目录文件


目录 (*类*) 文件包含属于 [驱动程序包](driver-packages.md)的所有文件的数字签名。 有关详细信息，请参阅 [编录文件](catalog-files.md)。

可以通过两种方法创建 [目录文件](catalog-files.md)：

-   如果驱动程序包是通过 INF 文件安装的，请使用 [**Inf2Cat**](../devtest/inf2cat.md) 工具创建编录文件。 Inf2Cat 自动包括在包的 INF 文件中引用的驱动程序包中的所有文件。 有关如何使用 Inf2Cat 工具的详细信息，请参阅 [使用 Inf2Cat 创建编录文件](using-inf2cat-to-create-a-catalog-file.md)。

-   如果未通过 INF 文件安装驱动程序包，请使用 [MakeCat](/windows/win32/seccrypto/makecat) 工具，通过使用手动创建的目录定义文件 (*cdf*) 来创建目录文件。

    例如，如果驱动程序包是通过应用程序安装的，则可能要创建一个编录文件来对包的所有内核模式二进制组件进行数字签名，如驱动程序和任何支持 *.dll* 文件。 有关如何使用 MakeCat 工具的详细信息，请参阅 [使用 MakeCat 创建编录文件](using-makecat-to-create-a-catalog-file.md)。

安装以下类型的驱动程序不需要目录文件：

-   *启动启动驱动程序*。

-   使用不使用 [目录文件](catalog-files.md)的应用程序安装的驱动程序。

对于这些类型的驱动程序，必须将数字签名嵌入驱动程序中。 有关此过程的详细信息，请参阅 [通过嵌入签名对驱动程序进行测试签名](test-signing-a-driver-through-an-embedded-signature.md)。

有关如何创建目录文件的详细信息，请参阅为 [Test-Signed 驱动程序包创建编录文件](creating-a-catalog-file-for-a-test-signed-driver-package.md)。

