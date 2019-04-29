---
title: 创建用于对驱动程序包进行测试签名的目录文件
description: 创建用于对驱动程序包进行测试签名的目录文件
ms.assetid: 0bbb4dfa-d203-4618-946e-95d2896081ac
keywords:
- 测试签名驱动程序包 WDK，目录文件
- 目录文件 WDK 驱动程序签名，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42b77d0715a981ffdfa69518f087f55420f4f6fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364342"
---
# <a name="creating-a-catalog-file-for-test-signing-a-driver-package"></a>创建用于对驱动程序包进行测试签名的目录文件


目录 (*.cat*) 文件包含的所有文件都是一部分的数字签名的[驱动程序包](driver-packages.md)。 有关详细信息，请参阅[目录文件](catalog-files.md)。

有两种方法来创建[编录文件](catalog-files.md):

-   如果通过 INF 文件安装的驱动程序包，则使用[ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)工具创建目录文件。 Inf2Cat 自动包含在包的 INF 文件中引用的驱动程序包中的所有文件。 有关如何使用 Inf2Cat 工具的详细信息，请参阅[使用 Inf2Cat 创建编录文件](using-inf2cat-to-create-a-catalog-file.md)。

-   如果通过 INF 文件未安装驱动程序包，则使用[MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)工具，用于通过使用手动创建目录定义文件创建编录文件 (*.cdf*)。

    例如，如果通过应用程序安装的驱动程序包，则您可能想要创建编录文件进行数字签名的包，如驱动程序以及任何支持的所有内核模式二进制组件 *.dll*文件。 有关如何使用 MakeCat 工具的详细信息，请参阅[使用 MakeCat 创建编录文件](using-makecat-to-create-a-catalog-file.md)。

目录文件时不需要安装以下类型的驱动程序：

-   一个*引导启动驱动程序*。

-   通过使用不使用的应用程序安装的驱动程序[编录文件](catalog-files.md)。

对于这些类型的驱动程序，您必须嵌入在驱动程序中的数字签名。 有关此过程的详细信息，请参阅[测试签名的驱动程序通过嵌入式签名](test-signing-a-driver-through-an-embedded-signature.md)。

有关如何创建目录文件的详细信息，请参阅[为 Test-Signed 驱动程序包创建编录文件](creating-a-catalog-file-for-a-test-signed-driver-package.md)。

 

 





