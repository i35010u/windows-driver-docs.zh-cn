---
title: 为驱动程序签名以便公开发布
description: 为驱动程序签名以便公开发布
ms.assetid: 29e465b4-42f2-4c41-afa7-3f0adf579b0c
keywords:
- 驱动程序签名 WDK，公开发布的版本
- 签名的驱动程序 WDK，公共释放
- 数字签名 WDK，公共版本
- WDK 中公共签名版本
- 公开发布的版本驱动程序签名 WDK
- 签名 WDK 版本
- 公开发布的版本驱动程序签名 WDK，释放签名
- 发布有关版本签名签名 WDK，
- 发布签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef269a55dd9be31ec269a4218c3f1153531cf228
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564177"
---
# <a name="signing-drivers-for-public-release"></a>为驱动程序签名以便公开发布


版本签名标识的内核模式二进制文件的发布服务器 (例如，驱动程序或 *.dll*)，将加载到 Windows Vista 和更高版本的 Windows。 内核模式二进制文件是通过已发布签名：

-   一个[WHQL 版本签名](whql-release-signature.md)通过获得[Windows 徽标计划](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver)。

-   通过创建版本签名[软件发布者证书 (SPC)](software-publisher-certificate.md)。

若要了解版本签名中所涉及的步骤[驱动程序包](driver-packages.md)，查看以下主题：

<a href="" id="introduction-to-release-signing"></a>[版本签名简介](introduction-to-release-signing.md)  
本主题介绍是重要的是，发布签署驱动程序包的原因，并提供高级的版本签名过程的摘要。

<a href="" id="how-to-release-sign-a-driver-package"></a>[如何发布签名的驱动程序包](how-to-release-sign-a-driver-package.md)  
本主题提供版本签名过程的高级概述并介绍许多版本签名的示例通过使用*ToastPkg*示例驱动程序包中 Windows Driver Kit (WDK)。

有关版本签名过程的详细信息，请参阅以下主题：

[WHQL 版本签名](whql-release-signature.md)

[发布证书](release-certificates.md)

[版本签名驱动程序包](release-signing-driver-packages.md)

 

 





