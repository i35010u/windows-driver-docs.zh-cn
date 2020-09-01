---
title: 生成固件包并将其提交到 Windows 更新 (WU)
description: 生成固件包并将其提交到 Windows 更新 (WU)
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 455bcbadeab91047878a0444d5eda23eef5bdbe6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186045"
---
# <a name="build-and-submit-a-firmware-package-to-windows-update-wu"></a>生成固件包并将其提交到 Windows 更新 (WU)

由于固件更新作为驱动程序包提供，因此它将遵循与设备驱动程序包相同的验证和签名过程。

1. 如果驱动程序包的内容安装在 (SUT) 测试的系统上，则设备必须通过所需的 Windows 硬件实验室工具包 (HLK) 测试。 如果没有专用于正在测试的固件的测试，请找到最合理的替代项，并根据需要提交针对 HLK 包的结果。

2. 然后，可以将驱动程序包提交到 [合作伙伴中心](https://partner.microsoft.com/dashboard) 进行签名。

3. 签名后，会向提交者提供驱动程序包，其中提交者可选择使用驱动程序分发功能) Windows 更新 (WU) 通过硬件仪表 (板进行发布。

使用驱动程序分发功能通过 [硬件仪表板](https://partner.microsoft.com/dashboard) 发布到 Windows 更新。

驱动程序包的签名不同于对 UEFI 固件进行签名，但两者都需要签名。 使用文件签名服务功能通过硬件仪表板进行签名。 驱动程序包上的签名（通过安全目录提供）在将其处理到 UEFI 之前，由 Windows 用于验证其完整性。 Windows 不向固件提供安全目录。 UEFI 固件或设备固件更新上的签名由平台固件验证，Windows 不检查该签名。 IHV 或 OEM 负责通过签名验证、加密或其他方式来确保固件的完整性和安全性。 有关更多详细信息，请查看下面的 [MICROSOFT UEFI CA 签名策略更新](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification) 链接。

接下来，签署胶囊的内容。 胶囊内容本身由 OEM 决定。 胶囊可能只包含一个要使用 OEM 所选择的格式更新的固件映像目录，或以 EFI 应用程序图像形式提供 (PE/COFF 文件格式) 。 如果胶囊是 PE/COFF 文件，则它必须由 OEM 签名，然后才能提交给 Microsoft 以进行 Windows 固件更新包签名。

在基于 ARM 的系统上，在 UEFI 允许的数据库中不允许使用除 Microsoft 生产 CA 2011 以外的任何密钥，Microsoft 不会使用此 CA 下的签名者对第三方 UEFI 代码进行签名，因此，此类胶囊的负载无法利用常规 UEFI **LoadImage ( # B1 ** 服务。 不过，可以使用特定于平台的验证针对启动 ROM 公钥或 UEFI PK 加载胶囊应用程序。 \[对于任何其他映像，此负载仍必须按 TPM PCR 7 进行度量 \] 。 一般来说，在需要胶囊签名时 (例如，若要确保) 的完整更新包的完整性和真实性，并且胶囊可以包含 UEFI 外部固件的固件更新，则应将胶囊签名为可以使用平台持有的非 UEFI 密钥进行验证 (例如，使用密钥链接返回到连接到启动 ROM 或 UEFI PK) 的公钥进行签名。

![驱动程序签名工作流](images/driver-signing-workflow.png)

在非 ARM 系统上，

- 此胶囊可以是 EFI 应用程序，前提是该应用程序已使用返回到 UEFI 允许数据库中的条目的密钥链接进行签名。

- 然后，可以自动利用 UEFI 安全启动来验证胶囊的完整性。

> [!NOTE]
> 即使在测试环境中，Windows 也不允许 OEM Verisign 签名固件更新包。 它们必须由 Microsoft 通过门户进行签名。

通过安装固件更新包更新 SUT 设备上的固件。

在带有 PTP 的测试系统上 (HLK) 安装 Windows 硬件实验室工具包，并运行适用于该固件设备的所有测试。将 *HLK 日志和驱动程序包* 提交到合作伙伴中心进行签名。

> [!NOTE]
> 提交固件更新驱动程序包时，请确保选择 Windows 8 或更高版本作为适用的操作系统。 如果选择了任何下级操作系统，则合作伙伴中心将对包含 SHA1 算法的驱动程序包中的目录进行签名。 从 Windows 8 开始，必须对所有固件更新驱动程序包进行 SHA256 签名。

尽管不建议这样做，但在提交) 时，无需先生成 (或包括 HLK 测试日志的 HLK 测试日志，就可以将包提交给 Microsoft。 在不使用 HLK pass 测试日志或用于验证测试的情况下，对驱动程序签名使用 " **创建驱动程序签名提交** "。

无需 HLK 测试日志的驱动程序签名的要求是以 CAB 格式提交驱动程序。

使用内置 Makecab.exe 允许用户创建 CAB 文件。 尽管还有其他工具 (例如 Cabarch.exe) 可用，但有时查找和不包含在包装盒中会更难。

关键是要确保包含驱动程序的文件夹也包含在 CAB 文件中。 例如，驱动程序包的结构可能类似于以下内容：

```syntax
C:\Desktop
        \DriverFolderOne
                Driver.inf
                Driver.sys
```

如果遵循此格式，则提交应通过。 若要确认父文件夹已成为 CAB，请在 Windows 资源管理器中打开 CAB，并将 **视图** 切换到 " **详细信息**"。 将存在一个不应为空的 **路径** 列。

## <a name="related-resources"></a>相关资源

[创作固件更新包](./authoring-a-firmware-update-package.md)

[认证和签署更新包](./certifying-and-signing-the-update-package.md)

[Device.Fundamentals 可靠性测试先决条件](/windows-hardware/test/hlk/testref/devicefundamentals-reliability-testing-prerequisites)

[驱动程序签名](../dashboard/index.yml)

[Microsoft UEFI CA 签名策略更新](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)

[查看测试结果和日志文件](/windows-hardware/test/hlk/getstarted/step-7-view-test-results-and-log-files)

[创建提交包](/windows-hardware/test/hlk/getstarted/step-8-create-a-submission-package)

[通过固件驱动程序包进行的系统和设备固件更新](./system-and-device-firmware-updates-via-a-firmware-driver-package.md)

[使用 Windows HLK 排查设备基本组件可靠性测试问题](/windows-hardware/test/hlk/testref/troubleshooting-device-fundamentals-reliability-testing-by-using-the-windows-hck)

[Windows 硬件认证博客](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)

[Windows UEFI 固件更新平台](./windows-uefi-firmware-update-platform.md)

[合作伙伴中心](https://partner.microsoft.com/dashboard)

[ESRT 表定义 ](./esrt-table-definition.md)