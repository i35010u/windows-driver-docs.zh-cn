---
title: " (Vista 和更高版本的数字签名和 PnP 设备安装) "
description: 'Windows Vista 和更高版本 (的数字签名和 PnP 设备安装) '
ms.assetid: 38d3e8c9-0be1-4fea-9128-15834c0c4e2e
keywords:
- 驱动程序签名 WDK，PnP 设备安装
- 对驱动程序进行签名 WDK，PnP 设备安装
- 数字签名 WDK，PnP 设备安装
- 签名 WDK，PnP 设备安装
- PnP WDK 驱动程序签名
- 即插即用 WDK 驱动程序签名
- 驱动程序包数字签名 WDK
- 包数字签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a2d60aaaa644893e329d57e0f51cff984a713da
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095227"
---
# <a name="digital-signatures-and-pnp-device-installation-windows-vista-and-later"></a>Windows Vista 和更高版本 (的数字签名和 PnP 设备安装) 


在 Windows Vista 和更高版本的 Windows 上，即插即用 (PnP) 设备安装使用[驱动程序包](driver-packages.md)的 [目录文件](catalog-files.md)的[数字签名](digital-signatures.md)来执行以下操作：

-   验证驱动程序包的发行者的标识。 Windows 使用标识来允许用户选择是否信任驱动程序的发布者。

-   确定在发布驱动程序包后是否对其进行了更改。

Windows Vista 和更高版本的 Windows 上的 PnP 设备安装支持以下类型的 [驱动程序包](driver-packages.md)数字签名：

-   可用于发布到一般公共的驱动程序的签名类型：
    -   Windows 签名颁发机构生成的签名：
        1.  收件箱驱动程序
        2.  通过 Windows 硬件质量实验室对驱动程序进行认证和签名 (WHQL) 
        3.  Windows 持续工程 (SE) 更新。
    -   不是由 Windows 签名颁发机构生成的签名，但符合以下要求：

        1.  64位版本的 windows Vista 和更高版本的 Windows 的 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 。
        2.  Windows Vista 和更高版本的 windows 版本的 [PnP 设备安装签名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) 64 32 要求。

        这种类型的签名通过使用 [软件发行者证书 (SPC) ](software-publisher-certificate.md) ，该证书从 Microsoft 授权的第三方证书颁发机构 (CA) 获取此类证书。

    -   不是由 Windows 签名颁发机构生成且不符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)的签名，但符合 [PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。 此类型的签名可用于为32位版本的 Windows Vista 和更高版本的 Windows 的内核模式驱动程序签名。 这种类型的签名通过使用从属于 Microsoft 根证书程序成员的 CA 获得的 [商业发行证书](commercial-release-certificate.md) 生成。

-   仅在公司网络环境中部署驱动程序的签名，该证书由企业 CA 创建和管理的数字证书创建。 有关如何配置企业 CA 的详细信息不在本文档的讨论范围内。

    有关如何创建企业 CA 的信息，请参阅 [Windows 网站驱动程序签名要求](https://go.microsoft.com/fwlink/p/?linkid=14507) 中的 "代码签名最佳做法" 白皮书。

-   开发和测试驱动程序时可在内部使用的签名类型：
    -   由[WHQL 测试签名计划](whql-test-signature-program.md)生成的签名
    -   [MakeCert 测试证书](makecert-test-certificate.md)生成的签名
    -   由 [商业测试证书](commercial-test-certificate.md) 创建的签名，该证书是从 Microsoft 根证书程序成员的 CA 获得的
    -   [企业 CA 测试证书](enterprise-ca-test-certificate.md)生成的签名

Windows Vista 和更高版本的 Windows 包含以下功能，这些功能为第三方生成的签名提供支持：

-   管理员可以控制信任哪些驱动程序发布者。 Windows Vista 和更高版本的 Windows 在不提示的情况下从受信任的发行者安装驱动程序。 它永远不会从管理员选择不信任的发布者安装驱动程序。

-   驱动程序签名策略始终设置为 " *警告*"。 这消除了 Windows Server 2003、Windows XP 和 Windows 2000 中提供的 *忽略* 和 *阻止* 选项。 管理员必须始终向尚未受信任的发布者授权安装未签名的驱动程序或驱动程序。

-   所有 [设备安装程序类](./overview-of-device-setup-classes.md) 都平等对待。 在 Windows Server 2003、Windows XP 和 Windows 2000 上，WHQL 签署的驱动程序包必须有一个 INF 文件，该文件指定在 *% SystemRoot%/inf/Certclas.inf*中定义的设备安装程序类。 否则，Windows 会将驱动程序包视为无符号。

-   从 Windows Vista 开始，当有多个兼容的驱动程序可供选择时，操作系统用于选择最佳驱动程序的排名算法包括具有第三方签名的驱动程序。

    此算法通过以下方式对驱动程序进行排名：

    -   如果禁用了 [AllSignersEqual 组策略](./allsigningequal-group-policy.md) ，则会将使用 Microsoft 签名进行签名的驱动程序的操作系统排名高于使用第三方签名进行签名的驱动程序。 即使使用第三方签名进行签名的驱动程序是以更好的方式匹配设备，也会出现此排名。
    -   如果启用了 [AllSignersEqual 组策略](./allsigningequal-group-policy.md) ，则操作系统将对所有数字签名的驱动程序进行平均排名。

    **注意**   从 Windows 7 开始，默认情况下会启用[AllSignersEqual 组策略](./allsigningequal-group-policy.md)。 在 Windows Vista 和 Windows Server 2008 中， **AllSignersEqual** 组策略默认情况下处于禁用状态。 IT 部门可以通过启用或禁用 **AllSignersEqual** 组策略来覆盖默认排名行为。

     

安装驱动程序之前，Windows 会分析 [驱动程序包的](driver-packages.md) 数字签名。 如果存在签名，则 Windows 将使用该签名来验证驱动程序包中的文件。 根据此分析的结果，Windows 会按如下所示对数字签名进行分类：

-   **由 Windows 签名颁发机构签名。** 这些驱动程序包括在 Windows (默认安装的 Windows *收件箱驱动程序*) 中，由 WHQL 签署，或由 Windows SE 签名。

-   **由受信任的发布者签名。** 这些驱动程序已由第三方签署，用户已明确选择始终信任此发布者的签名驱动程序。

-   **由不受信任的发布者签名。** 这些驱动程序已由第三方签署，用户已明确选择从不信任此发布者提供的驱动程序。

-   **由未知信任的发布者签名。** 这些驱动程序已由第三方签名，并且用户未指明是否信任此发布者。

-   **改动.** 这些驱动程序已签名，但 Windows 检测到 [驱动程序包](driver-packages.md) 中的至少一个文件在包签名后被更改。

-   **无符号.** 这些驱动程序未签名或签名无效。 有效的签名必须使用由受信任的 CA 颁发的证书创建。

从 Windows Vista 开始，当操作系统首次在计算机上安装驱动程序时，它将预安装或阶段，驱动程序 [存储区](driver-store.md)中的驱动程序。 若要预安装驱动程序，Windows 会将驱动程序包复制到驱动程序存储区，并在系统 INF 目录中保存驱动程序包的 INF 文件的副本。 然后，Windows 将使用驱动程序存储区中驱动程序包的副本，以无提示方式为匹配的设备安装驱动程序。 当 Windows 安装预安装的设备驱动程序时，不需要用户交互。

Windows 是否将预安装 [驱动程序包](driver-packages.md) 取决于签名类别、用户凭据和用户交互，如下所示：

-   **由 Windows 签名颁发机构或受信任的发布者签名。** Windows 将以无提示方式预安装系统管理员和标准用户的驱动程序包)  (不具有管理员凭据的用户。 Windows 不显示任何用户对话框。

-   **由不受信任的发布者签名。** Windows 不预安装驱动程序包。

-   **由未知信任的发布者签名。** Windows 将向系统管理员显示一个对话框，通知管理员驱动程序包的发行者尚未受信任。 此对话框为管理员提供了安装驱动程序包的选项，以及用于始终信任发布者的选项。 Windows 不会向标准用户显示对话框，也不会为标准用户预装驱动程序包。

-   **已更改或未签名。** Windows 将显示一个对话框，该对话框会向系统管理员发出相应警告，指出无法验证签名。 此对话框为管理员提供了用于安装驱动程序包的选项。 Windows 不会向标准用户显示对话框，也不会为标准用户预装驱动程序包。

有关驱动程序签名和安装的详细信息，请参阅 [签名类别和驱动程序安装](signature-categories-and-driver-installation.md)。

 

