---
title: 软件发行者证书
description: 软件发行者证书
ms.assetid: eb06c630-9a3d-4f53-b00b-b1254c8bbaec
keywords:
- 目录文件 WDK 驱动程序签名，SPC
- 软件发行者证书 WDK 驱动程序签名
- SPC WDK 驱动程序签名
- 公共版本驱动程序签名 WDK、SPC
- release 签名 WDK，SPC
- 跨证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84cdd278cf87b72d7dad128fb2121dc268f16a80
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097089"
---
# <a name="software-publisher-certificate"></a>软件发行者证书


若要符合64位版本的 Windows 的 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) ，可以使用软件发行者证书 (SPC) 为内核模式驱动程序签名。 SPC 是从 Microsoft 授权的第三方证书颁发机构 () CA 颁发的，以颁发此类证书。 用这种类型的 SPC 生成的签名也符合 Windows 64 位和32位版本的 [PnP 驱动程序签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) 。

**注意**   适用于桌面版的 Windows 10 (家庭、专业版、企业版和教育版) 和 Windows Server 2016 内核模式驱动程序必须由 Windows 硬件开发人员中心仪表板进行签名，并且 Windows 硬件开发人员中心仪表板需要 EV 证书。 有关这些更改的详细信息，请参阅 [Windows 10 中的驱动程序签名更改](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)。

 > [!CAUTION] 
 > 从2021开始，大多数交叉证书都将开始过期。 这些交叉证书过期后，链接到这些交叉证书的代码签名证书将无法再创建新的内核模式数字签名。 这会影响 Windows 的所有版本。 有关详细信息，请参阅 [弃用软件发行者证书和商业发布证书](deprecation-of-software-publisher-certificates-and-commercial-release-certificates.md)。

## <a name="cross-certificates"></a>交叉证书

除了获取 SPC 外，还必须获取 Microsoft 颁发的交叉证书。 使用交叉证书来验证颁发 SPC 的 CA 是否为受信任的根证书颁发机构。 交叉证书是由 CA 颁发的 x.509 证书，用于对另一 CA 的根证书的公钥进行签名。 跨证书允许系统拥有单个受信任的 Microsoft 根证书颁发机构，还可以灵活地将信任链扩展到颁发 SPCs 的商业 Ca。

发布者不必使用 [驱动程序包](driver-packages.md)分发交叉证书。 交叉证书包含在驱动程序包的 [目录文件](catalog-files.md) 的数字签名或嵌入到驱动程序文件中的签名。 安装驱动程序包的用户无需执行任何其他配置步骤，因为使用了交叉证书。

有关提供 SPCs 的证书颁发机构的列表，以及有关交叉证书的详细信息，请参阅用于 [内核模式代码签名的交叉证书](./cross-certificates-for-kernel-mode-code-signing.md)。 按照证书颁发机构的网站上的说明，了解如何在要签署驱动程序的计算机上获取和安装 SPC 及相应的交叉证书。 此外，还必须将 SPC 信息添加到对驱动程序进行签名的本地计算机的 "个人" 证书存储中。 有关此要求的信息，请参阅在 [个人证书存储中安装 SPC 信息](#installing-spc-information-in-the-personal-certificate-store)。

## <a name="installing-spc-information-in-the-personal-certificate-store"></a>在个人证书存储中安装 SPC 信息

为了使用 SPC 对驱动程序进行签名的方式符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)的方式，必须首先将证书信息包含在个人信息交换 (*.pfx*) 文件中。 然后，必须将 *.pfx* 文件中包含的信息添加到对驱动程序进行签名的本地计算机的 "个人" 证书存储中。

CA 可能会颁发包含所需证书信息的 *.pfx* 文件。 如果是这样，您可以添加。*pfx* 文件保存到个人证书存储中，请按照在 [个人证书存储中安装 .pfx 文件](#installing-a-pfx-file-in-the-personal-certificate-store)中所述的说明进行操作。

但是，CA 可能会发出下列文件对：

-   一个包含私钥信息的 *pvk* 文件。

-   包含公钥信息的 *.spc* 或 *.cer* 文件。

在这种情况下，必须将*pvk*和 *.spc* *) 的* (文件对转换为 .pfx*文件，然后才能*将证书信息添加到个人证书存储 *.pfx*中，以便将证书信息添加到个人证书存储。

来创建。*pfx* 文件，请按照以下说明进行操作：

-   若要将 *pvk* 文件和 *.spc* 文件转换为 *.pfx* 文件，请在命令提示符处使用以下 [**Pvk2Pfx**](../devtest/pvk2pfx.md) 命令：

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc myspcfile.spc -pfx mypfxfile.pfx -po pfxpassword -f
    ```

-   若要将 *pvk* 文件和 *.cer* 文件转换为 *.pfx* 文件，请在命令提示符处使用以下 Pvk2Pfx 命令：

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc mycerfile.cer -pfx mypfxfile.pfx -po pfxpassword -f
    ```

下面介绍了 [**Pvk2Pfx**](../devtest/pvk2pfx.md) 命令中使用的参数：

-   **-Pvk**  *mypvkfile. pvk*参数指定*pvk*文件。

-   **-Pi**  *mypvkpassword*选项指定的密码。*pvk*文件。

-   **-Spc** *myspcfile*参数指定一个 *.spc*文件或 **-spc**  *mycerfile*参数指定 *.cer*文件。

-   **-Pfx** *mypfxfile*选项指定 *.pfx*文件的名称。

-   **-Po** *pfxpassword*选项指定 *.pfx*文件的密码。

-   **-F**选项将 Pvk2Pfx 配置为替换现有*的 .pfx*文件（如果存在）。

## <a name="installing-a-pfx-file-in-the-personal-certificate-store"></a>在个人证书存储中安装 .pfx 文件

从 CA 获取 *.pfx*文件或从*pvk*创建 *.pfx*文件后，也可以从。*spc*或 *.cer*文件，请将 *.pfx*文件中的信息添加到对驱动程序进行签名的本地计算机的 "个人" 证书存储中。 您可以使用证书导入向导将 *.pfx* 文件中的信息导入到个人证书存储，如下所示：

1.  在 Windows 资源管理器中找到 *.pfx* 文件，选择并按住 (或右键单击文件) ，然后选择 "打开" 以打开证书导入向导。

2.  按照证书导入向导中的步骤将代码签名证书导入到个人证书存储区中。


