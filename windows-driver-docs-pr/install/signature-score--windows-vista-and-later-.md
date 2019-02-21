---
title: 签名分数
description: 签名分数
ms.assetid: 5e8dbbf8-6282-4299-80d9-5f886d01b1bf
keywords:
- 签名分数 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e322655aab6d6b4b84cbe8dd3653a80a1932902
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534048"
---
# <a name="signature-score"></a>签名分数

此页介绍了 Windows 驱动程序的签名分数。 签名分数是三种评分包括在驱动程序级别之一。 此页上的信息仅适用于 Windows Vista 和更高版本的操作系统。

驱动程序级别的格式设置为 0x*SSGGTHHH*，其中值 0x*SS*000000 是签名的得分，值 0x00*GG*0000 是[功能分数](feature-score--windows-vista-and-later-.md)，和 0x0000 值*THHH*是[标识符分数](identifier-score--windows-vista-and-later-.md)。

签名分数进行排名的驱动程序根据签名驱动程序是如何，按如下所示：

-   Windows 将分配的最佳签名分数 （最低签名评分值） 具有受信任的签名的驱动程序。 这包括以下内容：

    -   高级 WHQL 签名和标准 WHQL 签名。
    -   收件箱驱动程序签名。
    -   Windows 可持续工程 (Windows SE) 签名。
    -   第三方签名使用验证码技术。  有效的第三方签名类型包括：
        -   使用代码签名证书从企业证书颁发机构 (CA) 签名的驱动程序。
        -   使用代码签名类 3 CA 颁发的证书签名的驱动程序。
        -   使用代码签名证书创建的驱动程序签名[ **MakeCert 工具**](https://msdn.microsoft.com/library/windows/hardware/ff548309)。
-   Windows 将分配到的第二个最佳签名分数[驱动程序包](driver-packages.md)不具有有效的签名，但情况下安装该驱动程序[ **INF *DDInstall*部分**](inf-ddinstall-section.md) ，其 **.nt**平台扩展。

    有关详细信息 **.nt**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

-   Windows 将第三个最佳签名分数分配给不具有有效签名的驱动程序包和驱动程序并不安装 INF *DDInstall*节，其中包含 **.nt**平台扩展。

-   Windows 将分配第四个和最差签名分数 （最高签名分数值） 驱动程序未签名的或其签名的状态是未知的。

有关驱动程序分级的详细信息，请参阅[如何 Windows Ranks Drivers](how-setup-ranks-drivers--windows-vista-and-later-.md)。

 

 





