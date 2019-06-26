---
title: 软件发行者证书
description: 软件发行者证书
ms.assetid: eb06c630-9a3d-4f53-b00b-b1254c8bbaec
keywords:
- 目录文件 WDK 驱动程序签名，SPC
- 软件发布者证书 WDK 驱动程序签名
- SPC WDK 驱动程序签名
- 公开发布的版本驱动程序签名 WDK，SPC
- 释放签名 WDK，SPC
- 交叉证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fafb1af6c37e3e8de4da2566d6089a0a7f58276
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393408"
---
# <a name="software-publisher-certificate"></a>软件发行者证书


若要符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)的 64 位版本的 Windows 中，可以通过使用软件发布者证书 (SPC) 签名的内核模式驱动程序。 从 Microsoft 授权颁发此类证书的第三方证书颁发机构 (CA) 获取 SPC。 使用这种类型的 SPC 生成的签名还遵守[即插即用驱动程序签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)64 位和 32 位版本的 Windows。

**请注意**  Windows 10 桌面版 （主页、 专业版、 企业版和教育版） 和 Windows Server 2016 内核模式驱动程序必须进行签名的 Windows 硬件开发人员中心仪表板和 Windows 硬件开发人员中心仪表板需要使用 EV 证书。 有关这些更改的详细信息，请参阅[Windows 10 中的驱动程序签名更改](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)。

 

## <a name="cross-certificates"></a>Cross-Certificates

除了获取一个 SPC，必须获取由 Microsoft 颁发交叉证书。 交叉证书用于验证颁发一个 SPC 的 CA 受信任的根颁发机构。 交叉证书是由另一个 CA 的根证书的公钥进行签名的 CA 颁发的 X.509 证书。 交叉证书允许系统在具有单个受信任的 Microsoft 的根颁发机构，但也提供灵活地扩展到商业 Ca 颁发 SPCs 的信任链。

发布服务器不需要分发与交叉证书[驱动程序包](driver-packages.md)。 交叉证书随数字签名的驱动程序包[编录文件](catalog-files.md)或驱动程序文件中嵌入的签名。 安装驱动程序包的用户无需执行引起的交叉证书的使用任何其他配置步骤。

提供 SPCs 的证书颁发机构的列表以及有关交叉证书的详细信息，请参阅[内核模式代码签名的交叉证书](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)。 有关如何获取并将登录驱动程序的计算机上安装的 SPC 和相应的交叉证书的证书颁发机构的网站上按照的说明。 此外，您必须将 SPC 信息添加到对进行签名的驱动程序在本地计算机的个人证书存储。 有关此要求的信息，请参阅[个人证书存储中安装 SPC 信息](#installing-spc-information-in-the-personal-certificate-store)。

## <a name="installing-spc-information-in-the-personal-certificate-store"></a>在个人证书存储中安装 SPC 信息

若要使用一个 SPC 进行签名的驱动程序符合的方式[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)，必须首先中个人信息交换中包含的证书信息 ( *.pfx*)文件。 中包含的信息 *.pfx*然后必须将文件添加到驱动程序进行签名的本地计算机的个人证书存储。

CA 可以颁发 *.pfx*文件，其中包含所需的证书信息。 如果因此，你可以添加。*pfx*中所述的说明的个人证书存储的文件[在个人证书存储中安装.pfx 文件](#installing-a-pfx-file-in-the-personal-certificate-store)。

但是，CA 可能会发出对以下文件：

-   一个 *.pvk*文件，其中包含私钥信息。

-   *.Spc*或 *.cer*文件，其中包含公钥信息。

在此情况下，对文件 ( *.pvk*和一个 *.spc，* 或 *.pvk*和一个 *.cer*) 必须转换为 *.pfx*若要将证书信息添加到个人证书存储的文件。

若要创建。*pfx*文件由 CA 颁发的对从文件中，按照这些说明进行操作：

-   要转换 *.pvk*文件和一个 *.spc*文件发送到 *.pfx*文件，请使用以下[ **Pvk2Pfx** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/pvk2pfx)在命令提示符的命令：

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc myspcfile.spc -pfx mypfxfile.pfx -po pfxpassword -f
    ```

-   要转换 *.pvk*文件和一个 *.cer*文件中，为 *.pfx*文件，请在命令提示符处使用以下 Pvk2Pfx 命令：

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc mycerfile.cer -pfx mypfxfile.pfx -po pfxpassword -f
    ```

以下描述中使用的参数[ **Pvk2Pfx** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/pvk2pfx)命令：

-   **-Pvk**  *mypvkfile.pvk*参数指定 *.pvk*文件。

-   **-Pi**  *mypvkpassword*选项指定的密码。*pvk*文件。

-   **-Spc** *myspcfile.spc*参数指定 *.spc*文件或 **-spc**  *mycerfile.cer*参数指定 *.cer*文件。

-   **-Pfx** *mypfxfile.pfx*选项指定的名称 *.pfx*文件。

-   **Po** *pfxpassword*选项指定的密码 *.pfx*文件。

-   **-F**选项配置 Pvk2Pfx 替换现有 *.pfx*文件如果存在。

## <a name="installing-a-pfx-file-in-the-personal-certificate-store"></a>在个人证书存储中安装一个.pfx 文件

获取后 *.pfx* CA，从文件或创建 *.pfx*从文件 *.pvk*并且。*spc*或 *.cer*文件中，添加中的信息 *.pfx*对进行签名的驱动程序在本地计算机的个人证书存储的文件。 您可以使用证书导入向导导入中的信息 *.pfx*文件到个人证书存储中，按如下所示：

1.  找到 *.pfx*文件位于 Windows 资源管理器，并双击要打开证书导入向导的文件。

2.  按照证书导入向导导入个人证书存储的代码签名证书中的过程。


 





