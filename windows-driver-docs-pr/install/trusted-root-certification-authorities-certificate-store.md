---
title: 受信任的根证书颁发机构证书存储
description: 受信任的根证书颁发机构证书存储
keywords:
- 证书存储 WDK
- 驱动程序签名 WDK，数字签名
- 受信任的根证书颁发机构证书存储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39b4513a2bfe2d2612b1599b2defcd488b50f5f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828579"
---
# <a name="trusted-root-certification-authorities-certificate-store"></a>受信任的根证书颁发机构证书存储


从 Windows Vista 开始，即插即用 (PnP) manager 在设备和驱动程序安装过程中执行驱动程序签名验证。 但是，仅当以下陈述为 true 时，PnP 管理器才能成功验证数字签名：

-   用于创建签名的签名证书由 (CA) 的证书颁发机构颁发。

-   CA 对应的根证书安装在 " *受信任的根证书颁发机构" 证书存储* 中。 因此，"受信任的根证书颁发机构" 证书存储包含 Windows 信任的所有 Ca 的根证书。

默认情况下，"受信任的根证书颁发机构" 证书存储区配置为满足 Microsoft 根证书计划要求的一组公共 Ca。 管理员可以配置默认的受信任 Ca 集，并安装其自己的私有 CA 用于验证软件。

**注意**  不太可能在网络环境以外信任私有 CA。

 

有效的数字签名可确保 [驱动程序包](driver-packages.md)的真实性和完整性。 但是，这并不意味着最终用户或系统管理员隐式信任软件发行者。 用户或管理员必须根据软件发布者和应用程序的知识，根据具体情况决定是按案例安装还是运行应用程序。 默认情况下，仅当发布者的证书安装在 " [受信任的发行者" 证书存储区](trusted-publishers-certificate-store.md)中时，它才受信任。

受信任的根证书颁发机构证书存储区的名称为 *Root。* 你可以使用 [**certmgr.msc**](../devtest/certmgr.md) 工具手动将专用 CA 的根证书安装到计算机上的 "受信任的根证书颁发机构" 证书存储中。

**注意**  PnP 管理器使用的驱动程序签名验证策略要求首先在 "根证书颁发机构" 证书存储的本地计算机版本中安装私有 CA 的根证书。 有关详细信息，请参阅 [Local Machine and Current User Certificate Stores](local-machine-and-current-user-certificate-stores.md)（本地计算机和当前用户证书存储）。



有关驱动程序签名的详细信息，请参阅 [驱动程序签名策略](./kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

 

