---
title: 测试签名简介
description: 测试签名简介
ms.assetid: 63d4627d-b92c-489d-accf-16cfb5ac1410
keywords:
- 测试签名驱动程序包 WDK，关于测试签名驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a5468fc8da73b9640eece3f47a900b79687b9a3
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096335"
---
# <a name="introduction-to-test-signing"></a>测试签名简介


在开发和测试过程中，应使用 [数字签名](digital-signatures.md) 对驱动程序进行测试签名，原因如下：

-   以便于和自动执行安装。

    如果未对驱动程序进行签名，则 Windows Vista 和更高版本的 Windows 的 [即插即用 (PnP) 驱动程序安装策略](digital-signatures-and-pnp-device-installation--windows-vista-and-late.md) 要求系统管理员手动授权安装未签名的驱动程序，并在安装过程中添加额外的步骤。 这一额外步骤可能会对开发人员和测试人员的工作效率产生负面影响。 此要求不能被重写。

-   在64位版本的 windows Vista 和更高版本的 Windows 上加载内核模式驱动程序。

    默认情况下，Windows Vista 和更高版本的 windows 版本的 [内核模式代码签名64策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 要求对内核模式驱动程序进行签名，以便加载驱动程序。 可以暂时重写此要求，以便于开发或调试驱动程序。

-   若要播放特定类型的下一代高级内容，Windows Vista 和更高版本的 Windows 中的所有内核模式组件都必须进行签名。 此外，受保护媒体路径 (PMP) 中的所有用户模式和内核模式组件必须符合 PMP 签名策略。 有关 PMP 签名策略的信息，请参阅 [Windows Vista 中的针对受保护媒体组件的白皮书代码签名](https://download.microsoft.com/download/a/f/7/af7777e5-7dcd-4800-8a0a-b18336565f5b/pmp-sign.doc)。

由于这些原因，Windows Vista 和更高版本的 Windows 的驱动程序应使用通过使用 Microsoft Authenticode 创建的数字证书进行测试签名。 此类数字证书称为 *测试证书* ，使用测试证书生成的签名被称为 *测试签名*。

**注意**   Windows Vista 和更高版本的 Windows 支持测试签名的驱动程序，仅用于开发和测试目的。 测试签名不得用于生产目的或向客户发布。

 

开发和测试团队可以参与 [Whql 测试签名计划](whql-test-signature-program.md)，在此计划中，Windows 硬件质量实验室 (whql) 将为 PnP [驱动程序包](driver-packages.md) 签名，以供测试之用。 或者，开发和测试团队可以管理自己的内部签名过程，并使用以下类型的 [测试证书](./makecert-test-certificate.md) 对驱动程序进行测试签名：

-   [MakeCert 测试证书](makecert-test-certificate.md)，该证书是由 [**MakeCert**](../devtest/makecert.md) 工具创建的数字证书。

-   [商业测试证书](commercial-test-certificate.md)，该证书是由作为 Microsoft 根证书程序成员的 CA 颁发的数字证书。

-   [企业 ca 测试证书](enterprise-ca-test-certificate.md)，它是企业 ca 部署的数字证书。

有关测试团队在团队创建、获取或提供测试证书后对驱动程序包进行签名的信息，请参阅 [测试签名驱动程序包](test-signing-driver-packages.md)。

有关如何安装经过测试签名的驱动程序包的信息，请参阅 [安装测试签名的驱动程序包](installing-test-signed-driver-packages.md)。

为了便于提前驱动程序开发和调试，你可以暂时禁用内核模式代码签名要求，以便加载和测试未签名的内核模式驱动程序。 但是，您不能禁用 PnP 驱动程序安装策略，要求系统管理员授权安装未签名的驱动程序。 有关如何安装未签名的驱动程序的详细信息，请参阅 [在开发和测试过程中安装未签名的驱动程序](installing-an-unsigned-driver-during-development-and-test.md)。

有关用于测试签名驱动程序包的最合适工具的信息，请参阅 [用于签署驱动程序的工具](../devtest/tools-for-signing-drivers.md)。

**注意**   若要更好地了解测试签名驱动程序包中涉及的步骤，请参阅如何对[驱动程序包进行测试签名](how-to-test-sign-a-driver-package.md)。 本主题提供了测试签名过程的摘要，并通过使用 Windows 驱动程序工具包 (WDK) 中的 *toastpkg.inf* 示例 [驱动程序包](driver-packages.md) ，逐步完成测试签名示例。

 

 

