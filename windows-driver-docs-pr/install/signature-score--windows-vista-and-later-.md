---
title: 签名分数
description: 签名分数
keywords:
- 签名评分 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52f853be0b6b993c3499cbb04b8e0d335017428
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838885"
---
# <a name="signature-score"></a>签名分数

此页介绍 Windows 驱动程序的签名评分。 签名分数是包含在驱动程序级别中的三个评分之一。 本页中的信息仅适用于 Windows Vista 和更高版本的操作系统。

驱动程序级别的格式设置为 0x *SSGGTHHH*，其中 0x *SS* 000000 的值是签名分数，0x00 *GG* 0000 的值是 [功能分数](feature-score--windows-vista-and-later-.md)，0x0000 *THHH* 的值是 [标识符分数](identifier-score--windows-vista-and-later-.md)。

签名分数根据驱动程序的签名方式对驱动程序进行排名，如下所示：

-   Windows 将 (最低签名分数值) 的最佳签名分数分配给具有受信任签名的驱动程序。 其中包括：

    -   高级 WHQL 签名和标准 WHQL 签名。
    -   收件箱驱动程序的签名。
    -   Windows (Windows SE) 签名的 windows 持续工程。
    -   使用 Authenticode 技术的第三方签名。  有效的第三方签名类型包括以下内容：
        -   使用企业证书颁发机构颁发的代码签名证书签名的驱动程序 (CA) 。
        -   使用类 3 CA 颁发的代码签名证书对驱动程序进行签名。
        -   使用 [**MakeCert 工具**](../devtest/makecert.md)创建的代码签名证书对驱动程序进行签名。
-   Windows 会将第二个最佳签名评分分配给没有有效签名的 [驱动程序包](driver-packages.md)，但该驱动程序由一个具有 **nt** 平台扩展的 [**INF *DDInstall* 部分**](inf-ddinstall-section.md)安装。

    有关 **nt** 扩展名的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

-   Windows 将第三个最佳签名评分分配给没有有效签名的驱动程序包，且该驱动程序不是由包含 **nt** 平台扩展的 INF *DDInstall* 部分安装的。

-   Windows 将第四个和最差的签名分数 (最高的签名分数值) 到未签名或其签名状态未知的驱动程序。

有关驱动程序排名的详细信息，请参阅 [Windows 如何对驱动程序](how-setup-ranks-drivers--windows-vista-and-later-.md)进行排名。

 

