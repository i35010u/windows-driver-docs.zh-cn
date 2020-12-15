---
title: 为驱动程序签名以便公开发布
description: 在公开发布驱动程序包之前，我们建议你先提交程序包以进行认证。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394564e2c6729a166c90529fe1199c2b7c829307
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784133"
---
# <a name="signing-a-driver-for-public-release"></a>为驱动程序签名以便公开发布

在公开发布驱动程序包之前，我们建议你先提交程序包以进行认证。 有关详细信息，请参阅 [Windows 硬件认证](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))和[硬件仪表板服务](../dashboard/index.yml)。 要提交驱动程序包以进行认证，你必须使用从受信任的证书颁发机构（如 VeriSign）那里获得的证书来为该程序包签名。 有关详细信息，请参阅[获取 VeriSign 证书](../dashboard/index.yml)。 你还需要由 Microsoft 提供的交叉证书。

假设你已从 Verisign 获得一对文件：一个私钥文件 (PVK) 和一个软件发布证书 (SPC)。 此外还假设你拥有 Microsoft Visual Studio 解决方案，其中包含一个名为 MyDriver 的驱动程序项目和一个名为 MyDriver Package 的驱动程序包项目。 若要为驱动程序包签名，请执行以下步骤。

1.  使用 [**Pvk2Pfx**](../devtest/pvk2pfx.md) 工具创建个人信息交换 (PFX) 证书。 **Pvk2Pfx** 工具会将你的 PVK 和 SPC 文件视为输入，并创建一个 PFX 文件。 在此练习中，假设 PFX 文件被命名为 MyCert.pfx。

    **注意** 创建 PFX 文件后，你可以将其重复用于其他驱动程序项目并在其他驱动程序开发计算机上使用。
2.  要确定需要使用的交叉证书，请参阅[适用于内核模式代码签名的交叉证书](../install/cross-certificates-for-kernel-mode-code-signing.md)。 验证所需的交叉证书是否位于 $(BASEDIR)\\CrossCertificates 下，其中 $(BASEDIR) 是 Windows 工具包的基目录（例如 c:\\Program Files (x86)\\Windows Kits\\8.0\\CrossCertificates）。 如果所需的交叉证书不在此处，请从 Microsoft 下载交叉证书，并将其复制到 $(BASEDIR)\\CrossCertificates。
3.  在 Visual Studio 中，打开包含 MyDriver 和 MyDriver Package 项目的解决方案。 如果“解决方案资源管理器”窗口尚未打开，请从“视图”  菜单中选择“解决方案资源管理器”  。 在“解决方案资源管理器”窗口中，选择并按住（或右键单击）程序包项目 MyDriver Package，然后选择“属性” 。

4.  在程序包的属性页中，导航到“配置属性”&gt;“驱动程序签名”&gt;“常规”。  在“签名模式”  下拉列表中，选择“生产签名”  。 对于“生产签名”  ，执行下列操作之一：

    -   输入签名证书所在的路径（例如 c:\\Certs\\MyCert.pfx）。
    -   选择“从文件中选择”  ，然后浏览到你的签名证书。
    -   选择“从应用商店中选择”  ，然后选择你先前导入证书应用商店的证书。

        **注意** 若要将证书导入应用商店，请选择并按住（或右键单击）证书文件（PFX 文件），然后选择“安装 PFX”。 按照“证书导入”向导中的说明进行操作。

        **注意** 如果你决定稍后使用不同的证书，请确保你的新证书已导入到证书应用商店中。 如果你选择“从文件中选择”  并浏览至新的证书，则新证书将会自动导入证书应用商店中。 但是，如果你手动输入新证书的路径，则它不会自动导入到证书应用商店中。 在此情况下，必须选择并按住（或右键单击）新证书文件，然后选择“安装 PFX”。
5.  在“驱动程序签名”&gt;“常规”属性页中，对于“TimeStampServer”  ，从下拉列表中选择时间戳服务器之一。 

    **注意** 如需使用下拉列表中的时间戳服务器之一，则在生成驱动程序包时，必须连接到 Internet。 如果在生成驱动程序包时需要与 Internet 断开连接，请清除“TimeStampServer”  字段。
6.  在程序包的属性页中，导航到“配置属性”&gt;“Inf2Cat”&gt;“常规”。  在“运行 Inf2Cat”  下拉列表中，选择“是”  。

7.  关闭程序包的属性页。
8.  选择并按住（或右键单击）驱动程序项目 MyDriver，然后选择“属性”
9.  在驱动程序的属性页中，导航到“配置属性”&gt;“驱动程序签名”&gt;“常规”。  将“TimeStampServer”  设为驱动程序包属性中所用的相同值。 将“签名模式”  设为“生产签名”  ，然后将“生产证书”  设为驱动程序包属性中所用的相同值。

10. 准备好生成驱动程序包时，请按 **F5**。 Visual Studio 将会自动为你的程序包和驱动程序文件签名。 如果已配置部署，则 Visual Studio 还会将已签名的驱动程序包部署到测试计算机。 有关详细信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](../gettingstarted/provision-a-target-computer-wdk-8-1.md)。

## <a name="span-idviewing_the_driver_package_filesspanspan-idviewing_the_driver_package_filesspanspan-idviewing_the_driver_package_filesspanviewing-the-driver-package-files"></a><span id="Viewing_the_driver_package_files"></span><span id="viewing_the_driver_package_files"></span><span id="VIEWING_THE_DRIVER_PACKAGE_FILES"></span>查看驱动程序包文件


生成解决方案后，在文件资源管理器中导航至包含你的驱动程序包的文件夹。 程序包中的其中一个文件为目录文件。 该目录文件包含程序包的数字签名。 如需查看已签名程序包中的文件的示例，请参阅[基于模板编写 KMDF 驱动程序](../gettingstarted/writing-a-kmdf-driver-based-on-a-template.md)。

## <a name="span-idgetting_a_whql_release_signaturespanspan-idgetting_a_whql_release_signaturespanspan-idgetting_a_whql_release_signaturespangetting-a-whql-release-signature"></a><span id="Getting_a_WHQL_release_signature"></span><span id="getting_a_whql_release_signature"></span><span id="GETTING_A_WHQL_RELEASE_SIGNATURE"></span>获取 WHQL 发布签名


当驱动程序包通过认证测试时，可由 Windows 硬件质量实验室 (WHQL) 对其进行签名。 如果你的驱动程序包由 WHQL 进行签名，则可以通过 Windows 更新计划或其他 Microsoft 支持的分发机制来分发。

若要安装到 Windows 10、8.1、8 和 7 上，你的驱动程序包可以具有单个 SHA1 签名。

从 Windows 10 起，你还需要在 [Windows 硬件开发人员中心仪表板门户](https://msdn.microsoft.com/windows/hardware/gg236587.aspx)中提交任何新的 Windows 10 内核模式驱动程序以进行数字签名。  提交内核和用户模式驱动程序必须具有有效的[扩展验证 (“EV”) 代码签名证书](../dashboard/index.yml)。

**注意** SHA1 弃用不适用于驱动程序。  有关 Windows 中 SHA1 支持的结束日期信息，请参阅[验证码签名和时间戳的 Windows 强制](https://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-authenticode-code-signing-and-timestamping.aspx)。

## <a name="span-idsigning_a_package_compared_to_signing_an_individual_driver_filespanspan-idsigning_a_package_compared_to_signing_an_individual_driver_filespanspan-idsigning_a_package_compared_to_signing_an_individual_driver_filespansigning-a-package-compared-to-signing-an-individual-driver-file"></a><span id="Signing_a_package_compared_to_signing_an_individual_driver_file"></span><span id="signing_a_package_compared_to_signing_an_individual_driver_file"></span><span id="SIGNING_A_PACKAGE_COMPARED_TO_SIGNING_AN_INDIVIDUAL_DRIVER_FILE"></span>为程序包签名与为单个驱动程序文件签名的比较


驱动程序包中包含若干个文件。 通常情况下，驱动程序包具有一个或多个驱动程序文件、一个信息文件（INF 文件）和一个目录文件。 目录文件包含与程序包中的其他文件相关的信息。 为目录文件签名时，目录文件上的签名将用作整个驱动程序包的签名。 换言之，*为目录文件签名* 与 *为驱动程序包签名* 相同。

在大部分情况下，对驱动程序包进行签名即可，无需再对各个驱动程序文件进行签名。 但是，有时你需要对程序包和各个驱动程序文件进行签名。 例如，必须单独为引导启动驱动程序文件签名。 为单个驱动程序文件签名被称为 *在驱动程序文件中嵌入签名*。

假设你拥有 Visual Studio 解决方案，其中包含一个名为 MyDriver 的驱动程序项目和一个名为 MyDriver Package 的驱动程序包项目。 Visual Studio 提供有两个属性页：一个用于“我的驱动程序”，另一个用于“我的驱动程序包”。 若要为驱动程序包签名，请设置“我的驱动程序包”中的 **驱动程序签名** 属性。 若要在单个驱动程序文件中嵌入签名，请设置“我的驱动程序”中的 **驱动程序签名** 属性。

当你针对生产签名设置驱动程序包属性时，请记得相应地调整单个驱动程序文件的签名属性。 关闭单个驱动程序文件的签名，或者将单个驱动程序文件设为使用为程序包指定的相同证书。

**注意** 若要查看证书的哈希（也称为缩略图打印），请打开命令提示符窗口并导航至包含证书的目录。 输入命令 **certutil -dump** *CertName.pfx*，其中 *CertName.pfx* 为证书的名称。

     

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [Windows 10 中的驱动程序签名更改](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)
* [适用于 Windows 7 和 Windows Server 2008 R2 的 SHA-2 代码签名支持的可用性](/security-updates/SecurityAdvisories/2015/3033929)
* [为驱动程序签名](signing-a-driver.md)
* [Windows 硬件认证](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))
* [硬件仪表板服务](../dashboard/index.yml)
* [Windows 驱动程序签名要求](/previous-versions/windows/hardware/design/dn653563(v=vs.85))
* [用于内核模式代码签名的交叉证书](../install/cross-certificates-for-kernel-mode-code-signing.md)
* [内核模式代码签名演练](/previous-versions/windows/hardware/design/dn653569(v=vs.85))
* [驱动程序签名](../install/driver-signing.md)
* [安装引导启动驱动程序](../install/installing-a-boot-start-driver.md)
* [驱动程序签名工具](../devtest/tools-for-signing-drivers.md)
