---
title: 驱动程序签名工具
description: 驱动程序签名工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 360a74f41672c9f42100863b9445dfb8a93cdea6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805645"
---
# <a name="tools-for-signing-drivers"></a>驱动程序签名工具


Microsoft Windows 驱动程序工具包 (WDK) 包含以下工具，可用于创建代码签名证书、对[驱动程序包](../install/driver-packages.md)的[编录文件](../install/catalog-files.md)进行签名以及将签名嵌入驱动程序文件：

[**CertMgr**](certmgr.md)

[**Inf2Cat**](inf2cat.md)

[**MakeCat**](makecat.md)

[**MakeCert**](makecert.md)

[**Pvk2Pfx**](pvk2pfx.md)

[**SignTool**](signtool.md)

这些工具位于以下目录中：

-   Inf2Cat 工具位于% WindowsSdkDir% \\ bin \\ x86 目录中。

-   其他工具位于32位 Windows 平台 (% WindowsSdkDir% \\ bin \\ x86) 和64位 windows 平台 (% WindowsSdkDir% \\ bin \\ x64) 的目录中。

**注意**  Visual Studio 环境变量% WindowsSdkDir% 表示安装了此 WDK 版本的 Windows 工具包目录的路径，例如，C： \\ Program Files (x86) \\ Windows 工具包 \\ 10。

 

Microsoft Windows SDK 包含有关可用于向应用程序添加加密安全的服务、组件和工具的信息。 这包括 [**certmgr.msc**](certmgr.md)、 [**MakeCert**](makecert.md)和 [**SignTool**](signtool.md) 工具。

有关签名驱动程序和 [驱动程序包](../install/driver-packages.md)的详细信息，请参阅 [驱动程序签名](../install/driver-signing.md)。

有关对驱动程序包进行测试签名的信息，请参阅 [在开发和测试期间对驱动程序进行签名](../install/introduction-to-test-signing.md)。

 

