---
title: 认证和签署更新包
description: 固件更新作为驱动程序包提供，必须通过与常规驱动程序包相同的验证和签名过程。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6901cca9ca75533ddaf0fc96abdd7359bb7bf986
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803419"
---
# <a name="certifying-and-signing-the-update-package"></a>认证和签署更新包


由于固件更新是作为驱动程序包传送的，因此需要通过与常规驱动程序包相同的验证和签名过程。 驱动程序包需要将 Windows 硬件实验室工具包传递 (Windows HLK) 测试，并需要提交到合作伙伴中心进行签名。 签名后，驱动程序包将分发回提交者。

> [!NOTE]
> 驱动程序包的签名不同于对 UEFI 固件或设备固件本身进行签名。 驱动程序包上的签名（通过安全目录提供）在将其处理到 UEFI 之前，由 Windows 用于验证其完整性。 Windows 不向固件提供安全目录。 UEFI 固件或设备固件更新上的签名由平台固件验证，Windows 不检查该签名。 IHV/OEM 负责通过签名验证、加密或其他方式来确保固件的完整性和安全性。

## <a name="firmware-update-signing-process-and-requirements-for-uefi-secure-boot"></a>UEFI 安全启动的固件更新签名过程和要求

当对 UEFI 固件更新进行签名时，如果 Windows 设备使用 UEFI 安全启动，则签名过程会执行以下任务的一些组合：

1. )  (对更新的固件映像进行签名。
2. 为带有更新固件的胶囊进行签名。
3. 签署为操作系统提供的固件更新包;此包将包含胶囊。

在这些任务中， \# 始终只需要3个。 在启用安全引导的系统上，必须对所有 UEFI 固件进行签名，这意味着 \# 当更新涉及到 UEFI 驱动程序或应用程序时，需要1。 对于连接备用系统， \# 所有系统固件还需要1。 如果固件更新未通过其他方式进行保护，则必须对胶囊进行签名以保护固件更新本身，并确保更新包的真实性，然后再进行安装。

下图指示本主题的其余部分中讨论的各种组件的签名者。

![固件更新组件和签名者](images/firmwareupdatecomponentsandsigners.png)

## <a name="signing-the-updated-firmware"></a>签署更新的固件

签名后，必须能够在启动过程中通过系统固件加载程序来验证更新固件的签名。 至少，这会在重新启动时自动发生，但出于可靠性和用户体验的原因，强烈建议预先验证。

在 ARM 系统上，不能安装任何独立于固件映像本身的 UEFI 驱动程序或应用程序，因为唯一允许的 UEFI PE/COFF 映像是 (Bootmgfw.efi) 的 Microsoft Windows 操作系统加载程序，并且将使用包含 Microsoft Windows 生产 CA 2011 的唯一 UEFI 允许数据库项进行验证。 因此，只能添加系统和设备固件。 在非 ARM 系统上，UEFI 驱动程序和应用程序可以使用任何密钥链接进行签名，并将其返回到 UEFI 允许数据库中的密钥。

可以将系统或设备固件的密钥链接返回到绑定到系统启动 ROM 的密钥，或者通过其他方式 (例如，已签名的胶囊，然后受保护的安装) 。

## <a name="signing-the-capsule"></a>为胶囊签名

胶囊内容由 OEM 决定。 胶囊可能只包含一个要使用 OEM 所选择的格式更新的固件映像目录，或以 EFI 应用程序图像形式提供 (PE/COFF 文件格式) 。 如果胶囊是 PE/COFF 文件，则它必须由 OEM 签名，然后才能提交给 Microsoft 以进行 Windows 固件更新包签名。

在基于 ARM 的系统上，由于 UEFI 允许的数据库中不允许使用除 Microsoft 生产 CA 2011 以外的任何密钥 ( "db" ) ，因此 Microsoft 不会使用此 CA 下的签名者来签署第三方 UEFI 代码，因此此类胶囊的负载无法利用常规 UEFI LoadImage ( # A3 服务。 不过，可以使用特定于平台的验证针对启动 ROM 公钥或 UEFI PK 加载胶囊应用程序。 请注意，此负载仍必须在 TPM PCR 7 中测量为 \[ \] 适用于任何其他映像。 通常情况下，如果需要胶囊签名，则 (例如若要确保完整更新包) 的完整性和真实性，并且胶囊可以包含 UEFI 之外的固件的固件更新，则应将胶囊签名为可以使用平台持有的非 UEFI 密钥进行验证，例如，使用密钥链返回到连接 (到启动 ROM 或 UEFI PK) 的公钥进行签名。

在非 ARM 系统上，胶囊可以是 EFI 应用程序，前提是该应用程序已使用重新链接回 UEFI 允许数据库中的条目的密钥进行签名。 然后，可以自动利用 UEFI 安全启动来验证胶囊的完整性。

## <a name="signing-the-firmware-update-package"></a>签署固件更新包

需要将固件更新包提交到合作伙伴中心进行签名。 此步骤将创建包内容的目录签名。 目录签名由 Microsoft 操作系统加载程序用来验证包是否可信并且在实际更新通过 UpdateCapsule 提供给固件之前未被篡改。

将固件更新包提交到合作伙伴中心进行签名：

1. 按照上一部分中的说明签署胶囊的内容。
2. 创建包含胶囊的固件更新包，并对固件更新包进行测试签名。 有关详细信息，请参阅 [创作更新驱动程序包](authoring-an-update-driver-package.md)。
   > [!NOTE]
   > 从 Windows 8 开始，即使在测试环境中，Windows 也不允许 OEM 已签名的 azure 固件更新包。
3. 通过安装固件更新包更新固件。
4. 在测试系统上安装 Windows 硬件实验室工具包 (HLK) ，并运行适用于固件设备的所有测试。
5. 将 HLK 日志和驱动程序提交到合作伙伴中心进行签名。

> [!NOTE]
> 提交固件更新驱动程序包时，请确保选择 Windows 8 或更高版本作为适用的操作系统。 如果选择任何下级操作系统，则合作伙伴中心将用 SHA1 算法对驱动程序包中的目录进行签名。 从 Windows 8 开始，必须对所有固件更新驱动程序包进行 SHA256 签名。

## <a name="related-topics"></a>相关主题

[通过固件驱动程序包进行的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[填充 ESRT 表](populating-the-esrt-table.md)  
[自定义不同地理区域的固件](customizing-firmware-for-different-geographic-regions.md)  
[创作固件更新包](authoring-a-firmware-update-package.md)  
[安装更新](installing-the-update.md)  
