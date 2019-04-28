---
title: 受信任的根证书颁发机构证书存储
description: 受信任的根证书颁发机构证书存储
ms.assetid: c1969171-3691-4110-9530-693853728327
keywords:
- WDK 的证书存储
- 驱动程序签名 WDK，数字签名
- 受信任的根证书颁发机构证书存储区 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87c95dc9919eeae52a0ea904386afffeb6f3517e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339515"
---
# <a name="trusted-root-certification-authorities-certificate-store"></a>受信任的根证书颁发机构证书存储


从 Windows Vista 开始，插即用 (PnP) 管理器执行在设备和驱动程序安装过程中的驱动程序签名验证。 但是，即插即用管理器可以成功地验证数字签名，仅当以下语句为 true:

-   用于创建签名的签名证书是由证书颁发机构 (CA) 颁发的。

-   在安装相应的根证书的 ca*受信任的根证书颁发机构证书存储区*。 因此，受信任的根证书颁发机构证书存储区包含所有 Windows 信任的 Ca 的根证书。

默认情况下，使用一组已经满足 Microsoft 根证书计划的要求的公共 Ca 配置受信任的根证书颁发机构证书存储区。 管理员可以配置受信任的 Ca 的默认设置和安装其自己专用的 CA 验证软件。

**请注意**  专用 CA 不太可能在网络环境外部信任。

 

具有有效的数字签名的真实性和完整性可确保[驱动程序包](driver-packages.md)。 但是，它并不意味着最终用户或系统管理员隐式信任软件发行者。 用户或管理员必须决定是安装还是基于他们的知识的软件发布服务器和应用程序的情况的基础上运行应用程序。 默认情况下，发布者是受信任其证书在安装时才[受信任的发行者证书存储区](trusted-publishers-certificate-store.md)。

受信任的根证书颁发机构证书存储区的名称是*根。* 您可以手动安装专用的 CA 的根证书到受信任的根证书颁发机构证书存储区的计算机上使用[ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)工具。

**请注意**  驱动程序签名 PnP 管理器使用的验证策略需要是否以前已专用 CA 的根证书安装在本地计算机版本的根证书颁发机构证书存储区。 有关详细信息，请参阅[本地计算机和当前用户证书存储](local-machine-and-current-user-certificate-stores.md)。

 

证书存储区的详细信息，请参阅[驱动程序签名更改在 Windows 10，版本 1607年](https://blogs.msdn.microsoft.com/windows_hardware_certification/2016/07/26/driver-signing-changes-in-windows-10-version-1607/)并[驱动程序签名策略](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-policy--windows-vista-and-later-)。

 

 





