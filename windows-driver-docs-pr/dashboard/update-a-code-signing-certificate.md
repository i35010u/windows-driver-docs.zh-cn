---
title: 添加或更新代码签名证书
description: 添加或更新代码签名证书
ms.assetid: 120AA970-D981-4E7D-A9BD-68125D90A0EE
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11d35f1f576671440568259c0f0c42a886dd4f20
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337093"
---
# <a name="add-or-update-a-code-signing-certificate"></a>添加或更新代码签名证书

作为一名合作伙伴中心管理员，你负责保持数字证书信息处于最新状态。 原始证书过期时，你将需要获取新证书并上载使用你的新数字证书签名的新文件。

合作伙伴中心支持将多个证书与单个帐户相关联。  如果要添加其他证书，请使用这个相同的过程。

如果你首次在仪表板上注册公司，请参阅[建立新公司](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/establish-a-new-company)。

> [!IMPORTANT]
> 已上传并用于所有合作伙伴中心提交包的证书已更改：
>
> * **所有**提交都需要扩展验证 (EV) 代码签名证书。  
> * 所有证书都必须采用 SHA2 算法，并使用 **/fd sha256** signtool 命令行开关进行签名
> * （有关详细信息，请参阅此 [HLK 博客文章](https://blogs.msdn.microsoft.com/windows_hardware_certification/2017/11/13/starting-in-february-2018-packages-signed-using-a-sha-1-digest-algorithm-and-certificate-chain-will-no-longer-be-accepted/)）。

## <a name="to-add-or-update-a-code-signing-certificate"></a>添加或更新代码签名证书

### <a name="step-1-renew-your-code-signing-certificate-if-needed"></a>第 1 步：续订代码签名证书（如果需要）  

1. 确定所需的代码签名证书类型（有关详细信息，请参阅[获取代码签名证书](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/get-a-code-signing-certificate)）。

2. 获取新证书或重新使用现有的证书。

3. 从证书颁发机构收到已验证的证书后，继续执行**步骤 2** 以下载“Signablefile.bin”并为其签名

### <a name="step-2-sign-and-upload-your-signablefilebin-file"></a>步骤 2：为 Signablefile.bin 文件签名并将其上传

1. 仅允许**管理员**上传硬件仪表板证书或使其过期。

2. **管理员**登录后，你可以使用此直接链接[为文件签名并将其上传](https://partner.microsoft.com/dashboard/account/CertificateUpload)，或按照以下步骤手动导航到该页。

3. 单击右上角的齿轮图标，然后依次单击“开发人员设置”  和左窗格中的“管理证书”  。

4. 单击“添加新证书”  按钮，然后单击“下一步”  按钮。  

5. 下载 Signablefile.bin 并通过带有开关 **/fd sha256** 和相应 SHA-2 时间戳的 SignTool 使用公司的新数字证书为该文件签名。

6. 将已签名的文件上传到合作伙伴中心。

## <a name="related-topics"></a>相关主题

* [在登录之前](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/before-you-sign-in)

* [建立新公司](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/establish-a-new-company)

* [硬件认证提交](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/hardware-certification-submissions)

* [应用认证提交](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/app-certification-submissions)
