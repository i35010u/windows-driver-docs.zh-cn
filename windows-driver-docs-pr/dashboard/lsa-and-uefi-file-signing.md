---
title: LSA 和 UEFI 文件签名
description: LSA 插件和 UEFI 固件签名
ms.localizationpriority: medium
ms.topic: article
ms.date: 10/17/2018
ms.openlocfilehash: cafdaa3a12a23d36c1174c64f1367c70eb80fecf
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67393063"
---
# <a name="file-signing-lsa-plugins-and-uefi-firmware"></a>文件签名 LSA 插件和 UEFI 固件

使用合作伙伴中心，可以对[本地安全机构 (LSA)](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/configuring-additional-lsa-protection) 插件和 [UEFI 固件](https://docs.microsoft.com/windows-hardware/design/device-experiences/oem-uefi)二进制文件进行数字签名，使它们能够安装在 windows 设备上。

> [!IMPORTANT]
> 使用本主题所述的文件签名技术进行 **UEFI** 和 **LSA** 签名。
> 有关**驱动程序**签名的信息，请参阅[硬件提交](https://docs.microsoft.com/windows-hardware/drivers/dashboard/hardware-certification-submissions)。
>
> * 文件签名需要[扩展验证 (EV) 代码签名证书](get-a-code-signing-certificate.md)。
> * 所有 LSA 和 UEFI 提交均必须是已签名的单个 CAB 二进制文件，并包含签名所需的所有文件。
>   * 此文件不应包含任何文件夹，而只应包含要签名的二进制文件或 .efi 文件。
> * **仅 UEFI 固件** - CAB 文件签名必须与组织的[验证码证书](https://docs.microsoft.com/windows-hardware/drivers/install/authenticode)匹配。
>   * 视证书提供者而定，可能需要使用 [SignTool](https://docs.microsoft.com/windows/desktop/SecCrypto/signtool) 或外部进程。
>   * EFI ByteCode (EBC) 文件必须使用 /ALIGN:32 标志进行编译才能成功处理。
> * **仅 UEFI 固件** - 如果提交的是垫片，则必须向垫片审查委员会提交完整的模板以供审查。 垫片审查过程请参见 [https://github.com/rhboot/shim-review/](https://github.com/rhboot/shim-review/)。
> **仅 LSA 插件** - CAB 文件签名必须与组织的 EV 代码签名证书匹配。

## <a name="creating-a-new-uefi-or-lsa-submission"></a>创建新 UEFI 或 LSA 提交

1. 使用 Microsoft 帐户登录到仪表板，然后单击“硬件认证”  。

2. 在“文件签名服务”  页上，单击“提交新 UEFI”  或“提交新 LSA”  。
    > [!NOTE]
    > 在创建新的文件签名提交前，系统可能提示你签署法律协议。 请查看并签署协议以继续。 每个组织只需签署一次该协议。

3. 在提交页上，上传要提交的 CAB 文件，然后单击“提交”  。

4. 提交得到处理后，你将收到一条通知，其中包含提交 ID。

## <a name="managing-your-file-signing-submission"></a>管理文件签名提交

登录到合作伙伴中心后，可以[管理固件提交](manage-your-hardware-submissions.md)，方法与管理任何其他仪表板提交相同。

## <a name="related-topics"></a>相关主题

* [Microsoft UEFI CA 签名策略更新](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)

* [UEFI 提交的预提交测试](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)
