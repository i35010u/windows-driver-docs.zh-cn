---
ms.assetid: 1EBE8D0C-5F27-4FBE-8B0C-8AAD40F6FBC6
title: 在开发和测试期间签署驱动程序
description: 只有已签署的驱动程序包才能安装于 64 位 Windows 上。  出于测试目的，可以对驱动程序包进行测试签名。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c7184c3474fc9ca42ba7206ca7e5e62fc9828f9
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63378489"
---
# <a name="signing-a-driver-during-development-and-testing"></a>在开发和测试期间签署驱动程序

在运行 64 位版本 Windows 的计算机上安装驱动程序之前，必须先签署驱动程序包。 出于测试目的，可以对驱动程序包进行测试签名，这种签名形式比对公开发布进行的签名更为轻松。

在 Microsoft Visual Studio 中，默认已启用测试签名。 假设已按照[基于模板编写 KMDF 驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439654)中所述创建了一个 KMDF 驱动程序解决方案。 生成解决方案时，可以在“输出”  窗口中看到驱动程序包已完成测试签名。

![输出窗口的屏幕截图](images/SigningADriver01.png)

## <a name="span-idenablingtestsigningmanuallyspanspan-idenablingtestsigningmanuallyspanenabling-test-signing-manually"></a><span id="enabling_test_signing_manually"></span><span id="ENABLING_TEST_SIGNING_MANUALLY"></span>手动启用测试签名


若要手动启用测试签名，请执行以下步骤。

1.  在 Visual Studio 中，打开具有驱动程序包项目的解决方案。 右键单击驱动程序包项目，然后选择“属性”  。

2.  在程序包的属性页中，导航到“配置属性”&gt;“驱动程序签名”&gt;“常规”  。 在“签名模式”  下拉列表中，选择“测试签名”  。

3.  在程序包的属性页中，导航到“配置属性”&gt;“Inf2Cat”&gt;“常规”  。 在“运行 Inf2Cat”  下拉列表中，选择“是”  。

## <a name="span-idviewingthesigneddriverpackagespanspan-idviewingthesigneddriverpackagespanspan-idviewingthesigneddriverpackagespanviewing-the-signed-driver-package"></a><span id="Viewing_the_signed_driver_package"></span><span id="viewing_the_signed_driver_package"></span><span id="VIEWING_THE_SIGNED_DRIVER_PACKAGE"></span>查看已签名的驱动程序包


生成解决方案后，在文件资源管理器中导航至包含你的驱动程序包的文件夹。 程序包中的其中一个文件为目录文件。 该目录文件包含程序包的数字签名。 如需查看已签名程序包中的文件的示例，请参阅[基于模板编写 KMDF 驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439654)。

## <a name="span-idsharingasigningcertificatespanspan-idsharingasigningcertificatespanspan-idsharingasigningcertificatespansharing-a-signing-certificate"></a><span id="Sharing_a_signing_certificate"></span><span id="sharing_a_signing_certificate"></span><span id="SHARING_A_SIGNING_CERTIFICATE"></span>共享签名证书


对驱动程序包进行测试签名时，Visual Studio 将会创建一个签名证书（PFX 文件）并将其导入主计算机上的证书存储中。 将已完成测试签名的驱动程序包部署到测试计算机时，Visual Studio 会将验证证书（CER 文件）复制到测试计算机。 如果想要与在其他主计算机上生成驱动程序的开发人员共享证书，则必须共享签名证书，而不是验证证书。

若要共享签名证书，请执行以下步骤。

-   在 Visual Studio 的“解决方案资源管理器”窗口中，右键单击驱动程序包项目，然后选择“属性”  。
-   在程序包的属性页中，导航到“配置属性”&gt;“驱动程序签名”&gt;“常规”  。 在“测试证书”  字段中，选择“从 Microsoft Store 中选择”  。

-   在“选择证书”对话框中，找到测试签名证书。 证书名称类似于 WDKTestCert *yourName*。 选择测试签名证书，然后单击“属性”  。 在“详细信息”  选项卡中，单击“复制到文件”  。
-   按照“证书导出”向导中的说明导出 PFX 文件。 当系统询问你是否想要导出私钥时，选择“是，导出私钥”  。
-   与其他开发人员共享导出的 PFX 文件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [编写第一个驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554811)
* [生成驱动程序](building-a-driver.md)
* [开发、测试以及部署驱动程序](index.md)
 

 






