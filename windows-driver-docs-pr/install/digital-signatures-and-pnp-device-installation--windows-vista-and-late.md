---
title: 数字签名和即插即用设备安装 (Vista 及更高版本)
description: 数字签名和即插即用设备安装 (Windows Vista 及更高版本)
ms.assetid: 38d3e8c9-0be1-4fea-9128-15834c0c4e2e
keywords:
- 驱动程序签名 WDK，即插即用设备安装
- 签署驱动程序 WDK，即插即用设备安装
- 数字签名 WDK，即插即用设备安装
- 签名 WDK，即插即用设备安装
- 即插即用 WDK 驱动程序签名
- 插 WDK 驱动程序签名
- 驱动程序数据包数字签名 WDK
- 数据包数字签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ec2391559d7849351f58c43b594208956c0b18f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563319"
---
# <a name="digital-signatures-and-pnp-device-installation-windows-vista-and-later"></a>数字签名和即插即用设备安装 (Windows Vista 及更高版本)


插即用 (PnP) 设备安装在 Windows Vista 和更高版本的 Windows 上，使用[数字签名](digital-signatures.md)的[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)来执行操作以下：

-   验证驱动程序包的发布服务器的身份。 Windows 使用标识来允许用户选择是否要信任的驱动程序的发布服务器。

-   确定驱动程序包发布后对其已被更改。

在 Windows Vista 和更高版本的 Windows 上的即插即用设备安装支持以下类型的数字签名的[驱动程序包](driver-packages.md):

-   可用于向普通公众发布的驱动程序的签名类型：
    -   由签名颁发机构为 Windows 生成的签名：
        1.  收件箱驱动程序
        2.  认证和通过 Windows 硬件质量实验室 (WHQL) 签名的驱动程序
        3.  Windows 可持续工程 (SE) 更新。
    -   不由签名颁发机构，Windows 生成，但确实符合以下签名：

        1.  [内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)64 位版本的 Windows Vista 和更高版本的 Windows。
        2.  [PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)32 位和 64 位版本的 Windows Vista 和更高版本的 Windows。

        使用生成此类型的签名[软件发布者证书 (SPC)](software-publisher-certificate.md)从 Microsoft 授权颁发此类证书的第三方证书颁发机构 (CA) 获取。

    -   签名不由签名颁发机构 Windows 生成并不符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)，但确实符合[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。 可以使用这种类型的签名进行签名的 32 位版本的 Windows Vista 和更高版本的 Windows 内核模式驱动程序。 使用生成此类型的签名[商业版本发布证书](commercial-release-certificate.md)从此的 CA，则 Microsoft 根证书计划的成员。

-   有关部署驱动程序仅在企业网络环境中，这是创建和管理由企业 CA 的数字证书创建的签名。 本文档讨论了有关如何配置企业 CA 的详细的信息。

    有关如何创建企业 CA 的信息，请参阅"代码签名最佳实践"白皮书上[将签名要求驱动程序的 Windows](https://go.microsoft.com/fwlink/p/?linkid=14507)网站。

-   可以在开发和测试驱动程序的内部使用的签名类型：
    -   生成的签名[WHQL 测试签名的程序](whql-test-signature-program.md)
    -   生成的签名[MakeCert 测试证书](makecert-test-certificate.md)
    -   通过创建签名[商业测试证书](commercial-test-certificate.md)获取从 CA 的 Microsoft 根证书计划成员
    -   生成的签名[企业 CA 测试证书](enterprise-ca-test-certificate.md)

Windows Vista 和更高版本的 Windows 包括提供对由第三方生成签名的支持的以下功能：

-   管理员可以控制哪些驱动程序出版商的受信任。 Windows Vista 和更高版本的 Windows 安装驱动程序从受信任的发行者而不提示。 它永远不会从管理员已选择不信任的发布服务器中安装驱动程序。

-   驱动程序签名策略始终设置为*给出警告*。 这将消除*忽略*并*块*在 Windows Server 2003、 Windows XP 和 Windows 2000 中可用的选项。 管理员必须始终先授权未签名驱动程序或从尚不受信任的发布者的驱动程序的安装。

-   所有[设备安装程序类](device-setup-classes.md)同等对待。 在 Windows Server 2003、 Windows XP 和 Windows 2000 上，通过 WHQL 签名的驱动程序包必须具有指定的设备安装程序类中定义的 INF 文件 *%SystemRoot%/inf/Certclas.inf*。 否则，Windows 将视为未签名的驱动程序包。

-   Windows vista 中，从开始，当有多个兼容的驱动程序可供选择时，操作系统使用来选择最适合的驱动程序的排名算法包括具有第三方签名的驱动程序。

    此算法将驱动程序级别如下所示：

    -   如果[AllSignersEqual 组策略](allsignersequal-group-policy--windows-vista-and-later-.md)是禁用，操作系统进行排名使用具有第三方签名进行签名的驱动程序比更高版本的 Microsoft 签名进行签名的驱动程序。 即使使用第三方的签名进行签名的驱动程序是，在所有其他方面的更好地匹配设备会发生此排名。
    -   如果[AllSignersEqual 组策略](allsignersequal-group-policy--windows-vista-and-later-.md)是启用，操作系统同样排名数字签名的所有驱动程序。

    **请注意**  从 Windows 7 开始[AllSignersEqual 组策略](allsignersequal-group-policy--windows-vista-and-later-.md)默认情况下启用。 在 Windows Vista 和 Windows Server 2008 **AllSignersEqual**组策略在默认情况下处于禁用状态。 IT 部门可以重写默认排名行为通过启用或禁用**AllSignersEqual**组策略。

     

然后再安装一个驱动程序，Windows 会分析[驱动程序包的](driver-packages.md)数字签名。 如果存在签名，则 Windows 将使用签名的驱动程序包中对文件进行验证。 基于此分析的结果，Windows 将分类的数字签名，如下所示：

-   **由 Windows 签名颁发机构签名。** 这些驱动程序是否包括在 Windows 默认安装中 (*收件箱驱动程序*)、 通过 WHQL 版本签名或由 Windows SE 签名。

-   **由受信任的发行者签名。** 这些驱动程序已签署的第三方和用户已显式选择，以便始终信任来自此发布者签名的驱动程序。

-   **由不受信任的发布者签名。** 这些驱动程序已签署的第三方，并且用户已显式选永远不会信任来自此发布服务器的驱动程序。

-   **由未知的信任的发布者签名。** 这些驱动程序已签署的第三方，并在用户尚未指示是否信任此发布服务器。

-   **更改。** 这些驱动程序进行签名，但 Windows 检测到该至少一个文件中的[驱动程序包](driver-packages.md)包进行签名之后已更改。

-   **无符号。** 这些驱动程序为无符号或具有无效签名。 使用由受信任的 CA 颁发的证书，必须创建有效的签名。

从 Windows Vista 操作系统首次在计算机上安装的驱动程序时，在预安装，或暂存中的驱动程序[驱动程序存储区](driver-store.md)。 若要预安装了驱动程序，Windows 将驱动程序包复制到驱动程序存储区，并将驱动程序包的 INF 文件的副本保存在系统 INF 目录中。 Windows 随后将以无提示方式安装的驱动程序匹配的设备驱动程序存储区使用的驱动程序包副本。 Windows 安装设备的预安装驱动程序时，则不需要用户交互。

Windows 将预安装是否[驱动程序包](driver-packages.md)取决于签名类别、 用户凭据和用户交互，如下所示：

-   **由签名颁发机构或受信任的发行者 Windows 签名。** Windows 以无提示方式预安装的驱动程序包，面向系统管理员和标准用户 （用户不具有管理员凭据）。 Windows 不显示任何用户对话框。

-   **由不受信任的发布者签名。** Windows 预驱动程序包不安装。

-   **由未知的信任的发布者签名。** Windows 会通知管理员，将驱动程序包的发布服务器尚不受信任的系统管理员显示一个对话框。 安装驱动程序包的选项和用于始终信任发布者的选项，该对话框提供了管理员。 Windows 不向标准用户显示一个对话框，并不会预安装标准用户的驱动程序包。

-   **更改或无符号。** Windows 将显示一个对话框，适当地警告系统管理员无法验证签名。 对话框中提供管理员安装或未安装驱动程序包的选项。 Windows 不向标准用户显示一个对话框，并不会预安装标准用户的驱动程序包。

有关驱动程序签名和安装的详细信息，请参阅[签名类别和驱动程序安装](signature-categories-and-driver-installation.md)。

 

 





