---
title: 认证和签署更新包
description: 固件更新驱动程序包以交付，并且必须通过相同的验证和签名的进程作为常规驱动程序包。
ms.assetid: 054E98A5-E860-43BD-9AD2-7CCE55D2164B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1152a98b27d4a9d17a82374f37003d6b535c362f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328118"
---
# <a name="certifying-and-signing-the-update-package"></a>认证和签署更新包


由于固件更新为驱动程序包发送，因此，它将需要遍历所有相同的验证和签名的进程作为常规驱动程序包。 驱动程序包将需要通过 Windows 硬件实验室工具包 (Windows HLK) 测试，并且将需要将应用提交到合作伙伴中心进行签名。 签名之后，将回复到提交者分发驱动程序包。

> [!NOTE]
> 驱动程序包的签名与签名的 UEFI 固件或设备固件本身不同。 Windows 使用上通过安全目录提供的驱动程序包的签名以将其传递给 UEFI 之前验证 firmware.bin 的完整性。 Windows 不提供对固件的 security 目录。 UEFI 固件或设备固件更新的签名验证平台固件，并且不会检查 Windows。 IHV/OEM 负责确保完整性和安全性通过签名验证、 加密或其他方式的固件。

## <a name="firmware-update-signing-process-and-requirements-for-uefi-secure-boot"></a>固件更新签名过程和 UEFI 安全启动的要求

当面向消费 UEFI 安全启动活动的 Windows 设备的 UEFI 固件更新时，签名过程需要执行以下任务的某种组合：

1. 签名更新的固件映像。
2. 签名胶囊形执行已更新的固件。
3. 固件更新程序包进行签名提供给操作系统;此包将包含胶囊形。

这些任务，仅\#3 始终是必需。 在安全启用的系统上，所有的 UEFI 固件必须经过签名，这意味着\#1 时是必需的更新与 UEFI 驱动程序或应用程序。 对于已连接的备用系统， \#1 也是必需的所有系统固件。 固件更新未通过其他方式受到保护，以便保护固件更新本身并确保真实性的更新包安装之前，必须进行签名胶囊形。

下图表明此主题的其余部分中所述的各种组件的签名者。

![固件更新组件和签名者](images/firmwareupdatecomponentsandsigners.png)

## <a name="signing-the-updated-firmware"></a>签名更新的固件

签名后，已更新的固件的签名必须能够在启动过程中验证系统的固件加载程序。 至少，这将在重新启动时，会自动执行，但验证之前，强烈建议的可靠性和用户体验的原因。

在 ARM 系统上没有 UEFI 驱动程序或应用程序独立于固件映像本身可以安装因为唯一允许的 UEFI PE/COFF 映像是 Microsoft Windows 操作系统加载程序 (BootMgfw.efi)，并使用唯一的 UEFI 允许数据库项验证包含 Microsoft Windows 生产 CA 2011。 因此，可以添加仅系统和设备的固件。 在非 ARM 系统上可以使用任何密钥链接回 UEFI 允许数据库中的密钥签名 UEFI 驱动程序和应用程序。

系统或设备的固件或者使用链接后密钥签名到绑定到系统的密钥启动 ROM 或通过其他方式保护 (例如签名的 capsule，然后受保护的安装)。

## <a name="signing-the-capsule"></a>签名胶囊形

封装的内容由 OEM 决定。 Capsule 可能只包含固件映像中选择任何格式 OEM，要更新的目录或它可能会传送中的 EFI 应用程序图像 （PE/COFF 文件格式） 的窗体。 如果胶囊形是一个 PE/COFF 文件，然后它必须签名由 OEM 提交到 Microsoft 的 Windows 固件更新包签名之前。

在基于 ARM 的系统中，因为 UEFI 允许数据库 ("db") 中允许使用非 Microsoft 生产 CA 2011 没有密钥，Microsoft 不会使用在此 CA 的签名者第三方 UEFI 代码进行签名的此类 capsule 负载不能利用正则 UEFI LoadImage （) 服务。 但是，可能封装应用程序加载使用特定于平台的验证对启动 ROM 的公钥或 UEFI pk。 请注意，此负载必须仍要测量到 TPM PCR\[7\]与任何其他图像。 一般来说，当封装签名认为有必要 (例如以确保完成更新包的完整性和真实性)，和 capsule 可能包含外部 UEFI 固件的固件更新、 capsule 应登录此类可以是一种方法使用平台保留，验证非 UEFI 密钥 （例如使用签名密钥链接回公钥绑定到引导 ROM 或 UEFI PK）。

在非 ARM 系统上 capsule 可以是 EFI 应用程序，只要其签名与密钥链接回 UEFI 允许数据库中的条目。 UEFI 安全引导可以自动利用以验证胶囊形的完整性。

## <a name="signing-the-firmware-update-package"></a>固件更新程序包进行签名

固件更新包需要将应用提交到合作伙伴中心进行签名。 此步骤将创建目录签名的包的内容。 Microsoft 操作系统加载程序使用目录签名来验证包可信以及具有未被篡改之前执行实际的更新提供给通过 UpdateCapsule 固件。

提交到合作伙伴中心进行签名的固件更新包：

1. 登录 capsule 按照上一节中说明的内容。
2. 创建包括 capsule，固件更新包和测试对固件更新包进行签名。 有关详细信息，请参阅[创作更新驱动程序包](authoring-an-update-driver-package.md)。
   > [!NOTE]
   > 从 Windows 8 开始，Windows 不允许 OEM Verisign 签名固件更新包，即使在测试环境中。
3. 通过安装固件更新包更新固件。
4. 在测试系统上安装 Windows 硬件 Lab Kit (HLK) 并运行适用于固件设备的所有测试。
5. 提交 HLK 日志和到合作伙伴中心进行签名的驱动程序。

> [!NOTE]
> 在提交固件更新驱动程序包，请务必选择适用的操作系统为 Windows 8 或更高版本。 如果选择在任何低级别操作系统，合作伙伴中心将签名中使用 SHA1 算法的驱动程序包的目录。 从 Windows 8 开始，所有固件更新驱动程序包必须都是 SHA256 签名。

## <a name="related-topics"></a>相关主题

[通过固件驱动程序包的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[填充 ESRT 表](populating-the-esrt-table.md)  
[自定义不同的地理区域的固件](customizing-firmware-for-different-geographic-regions.md)  
[创作固件更新包](authoring-a-firmware-update-package.md)  
[安装更新](installing-the-update.md)  
