---
title: 生成固件包并将其提交到 Windows 更新 (WU)
description: 生成固件包并将其提交到 Windows 更新 (WU)
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 40d73866d11f451674744b2fcbb8e7676796234c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364594"
---
# <a name="build-and-submit-a-firmware-package-to-windows-update-wu"></a>生成固件包并将其提交到 Windows 更新 (WU)

由于固件更新为驱动程序包发送，因此，它遵循为设备驱动程序包的相同的验证和签名过程。

1. 驱动程序包的内容是安装在系统下测试 (SUT)，设备必须通过所需的 Windows 硬件 Lab Kit (HLK) 测试。 如果不是专门为固件所测试的测试，找到最合理的替代方案，并根据需要提交与 HLK 包的结果。

2. 驱动程序包然后提交到[合作伙伴中心](https://partner.microsoft.com/dashboard)进行签名。

3. 签名之后，驱动程序提供的包是向提交者提交者的已发布在 Windows Update (WU) 通过硬件仪表板的选项 （使用驱动程序分发功能）。

通过完成发布到 Windows 更新[硬件仪表板](https://partner.microsoft.com/dashboard)使用驱动程序分发功能。

尽管两者都需要进行签名，签名的驱动程序包是不同的签名 UEFI 固件。 签名是通过使用文件签名服务功能的硬件仪表板。 Windows 使用上通过安全目录提供的驱动程序包的签名以将其传递给 UEFI 之前验证 firmware.bin 的完整性。 Windows 不提供对固件的 security 目录。 在 UEFI 固件或设备固件更新的签名验证平台固件，并且不会检查 Windows。 IHV 或 OEM 负责确保完整性和安全性通过签名验证、 加密或其他方式的固件。 审阅[Microsoft UEFI CA 签名策略更新](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)下面链接的其他详细信息。

接下来，登录胶囊形的内容。 封装内容本身由 OEM 决定。 Capsule 可能只包含固件映像中选择任何格式 OEM，要更新的目录或它可能会传送中的 EFI 应用程序图像 （PE/COFF 文件格式） 的窗体。 如果 capsule 是 PE/COFF 文件，然后它必须签名由 OEM 提交到 Microsoft 的 Windows 固件更新包签名之前。

在基于 ARM 的系统中，与其他任何密钥不是 Microsoft 生产 CA 2011 中的 UEFI 允许数据库和 Microsoft 允许不使用在此 CA 的签名者第三方 UEFI 代码进行签名的此类 capsule 负载不能利用正则 UEFI **LoadImage()** 服务。 但是，可能封装应用程序加载使用特定于平台的验证对启动 ROM 的公钥或 UEFI pk。 此负载仍必须测量到 TPM PCR\[7\]与任何其他图像。 一般来说时封装签名认为 （例如，以确保完成更新包的完整性和真实性），有必要，capsule 可能包含外部 UEFI 固件的固件更新，, capsule 应为其登录的方式可以使用平台保留，验证非 UEFI 密钥 （例如，签名使用密钥链接返回到的公共密钥绑定启动 ROM 或 UEFI PK）。

![驱动程序签名工作流](images/driver-signing-workflow.png)

在非 ARM 系统上

- Capsule 可以是 EFI 应用程序，只要其签名与密钥链接回 UEFI 允许数据库中的条目。

- UEFI 安全引导可以自动利用以验证胶囊形的完整性。

> [!NOTE]
> 即使在测试环境中，Windows 不允许 OEM Verisign 签名固件更新包。 它们必须通过门户由 Microsoft 签名的测试。

通过安装固件更新包来更新你 SUT 的设备上的固件。

具有 PTP 的测试系统上安装 Windows 硬件 Lab Kit (HLK) 并运行适用于固件设备的所有测试。提交*HLK 日志和驱动程序包*到合作伙伴中心进行签名。

> [!NOTE]
> 在提交固件更新驱动程序包，请务必选择适用的操作系统为 Windows 8 或更高版本。 如果选择在任何低级别操作系统，则合作伙伴中心将签名中使用 SHA1 算法的驱动程序包的目录。 从 Windows 8 开始，所有固件更新驱动程序包必须都是 SHA256 签名。

尽管不建议使用，则可以提交给 Microsoft 而不首先生成 HLK 测试日志 （以后或提交时包括 HLK 测试日志） 的包。 使用**创建驱动程序签名提交**的驱动程序签名而无需 HLK 传递测试日志或验证测试。

驱动程序签名不含 HLK 测试日志的要求是在 CAB 格式中提交时，驱动程序。

在框 Makecab.exe 允许用户创建的 CAB 文件。 尽管有可用的其他工具 （如 Cabarch.exe)，它们是有时的详细信息难以找到并且不包含在框。

关键是确保包含该驱动程序的文件夹包含中的 CAB 文件。 例如，驱动程序包可能类似于以下的结构：

```syntax
C:\Desktop
        \DriverFolderOne
                Driver.inf
                Driver.sys
```

如果您遵循此格式，应传入提交。 若要确认进行到 CAB 的父文件夹，请在 Windows 资源管理器和开关打开 CAB**视图**到**详细信息**。 将有**路径**不应为空的列。

## <a name="related-resources"></a>相关资源

[创作固件更新包](https://docs.microsoft.com/windows-hardware/drivers/bringup/authoring-a-firmware-update-package)

[认证和签名的更新包](https://docs.microsoft.com/windows-hardware/drivers/bringup/certifying-and-signing-the-update-package)

[Device.Fundamentals 可靠性测试先决条件](https://docs.microsoft.com/windows-hardware/test/hlk/testref/devicefundamentals-reliability-testing-prerequisites)

[驱动程序签名](https://docs.microsoft.com/windows-hardware/drivers/dashboard)

[Microsoft UEFI CA 签名策略更新](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)

[查看测试结果和日志文件](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/step-7-view-test-results-and-log-files)

[创建提交包](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/step-8-create-a-submission-package)

[通过固件驱动程序包的系统和设备固件更新](https://docs.microsoft.com/windows-hardware/drivers/bringup/system-and-device-firmware-updates-via-a-firmware-driver-package)

[使用 Windows HLK 排查设备基本组件可靠性测试问题](https://docs.microsoft.com/windows-hardware/test/hlk/testref/troubleshooting-device-fundamentals-reliability-testing-by-using-the-windows-hck)

[Windows 硬件认证博客](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)

[Windows UEFI 固件更新平台](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-uefi-firmware-update-platform)

[合作伙伴中心](https://partner.microsoft.com/dashboard)

[ESRT 表定义 ](https://docs.microsoft.com/windows-hardware/drivers/bringup/esrt-table-definition)
