---
title: 合作伙伴中心常见问题解答
description: 本文提供了有关合作伙伴中心的常见问题解答。
ms.assetid: AA3D1147-7015-4D21-84A6-D127F57DDC97
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbc344aafeb335626b231013fb9dad398c2de185
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252989"
---
# <a name="hardware-dashboard-faq"></a>硬件仪表板常见问题

本文提供了有关合作伙伴中心的常见问题解答。

## <a name="contacting-partner-center-support"></a>联系合作伙伴中心支持部门

如果你在访问仪表板时遇到问题或需要仪表板支持，请在此处开具支持票证： https://developer.microsoft.com/windows/support 。  

如果有特定于帐户或提交的问题，则必须使用合作伙伴中心硬件仪表板用户名和密码登录。

依次选择“联系我们”  、“仪表板问题”  ，然后从下拉列表中选择“硬件提交和签名(所有 OS 版本)”  。  实时聊天和电子邮件支持时间为星期一至星期五上午 8 点到晚上 8 点（中部标准时间）。  电子邮件支持的初始响应 SLA 为 24-48 小时。

## <a name="can-i-associate-multiple-certificates-with-a-dashboard-account"></a>是否可以将多个证书与一个仪表板帐户关联在一起？

一个组织可以将多个证书与其仪表板帐户关联在一起。 必须使用这些证书中的任何一个对提交进行签名。

对与组织关联的证书（EV 和标准证书）数量没有限制。

## <a name="required-agreements-that-need-to-be-signed"></a>必须签署的协议

在注册过程中，可能会签署以下协议。

> [!NOTE]
> 所有注册都必须签署 Windows 兼容性计划和驱动程序质量证明测试协议。 其他所有协议都是可选的，除非你使用其他关联协议中所述的功能或资产。

* Windows 兼容性计划和驱动程序质量证明测试协议（2.0 版）

* Windows 徽标许可协议（2018 版）

* UEFI（统一可扩展固件接口）固件协议（1.0 版）

* Windows Analytics 协议（2.0 版）

* Microsoft 协作计划协议（1.0 版）

* Windows 桌面应用程序计划协议（1.0 版）

## <a name="adding-additional-users-or-grant-additional-roles-to-users-in-my-company"></a>添加其他用户或向公司中的用户授予其他角色

有关详细信息，请参阅[管理用户角色](managing-user-roles.md)。

## <a name="managing-submissions"></a>管理提交

### <a name="submission-processing-time-for-hardware-certification"></a>硬件认证的提交处理时间

提交到仪表板的硬件将在五个工作日或更少时间内进行处理，具体取决于提交是否需要手动检查。 如果提交测试失败、没有应用有效筛选器或由于内部业务策略的原因，可能需要手动检查。

### <a name="potential-differences-noticed-in-download-signed-files"></a>在下载的已签名文件中注意到的可能差异

为了使 Windows 10 更加安全并且性能不受影响，所有二进制文件现在均要接收嵌入式签名。 这适用于认证的所有提交，而不仅限于 Windows 10 提交。

### <a name="getting-a-single-cat-file-if-drivers-are-uniform-for-all-operating-systems"></a>在驱动程序对所有操作系统都统一的情况下获取单个 cat 文件

请在“程序包”  选项卡上确保最终的程序包具有单个驱动程序文件夹，并且该驱动程序的属性包含你已测试过的所有操作系统。 有关详细信息，请参阅[演练：如何获取由 Microsoft 签名的适用于多个版本的 Windows 的驱动程序](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)。

### <a name="adding-new-marketing-names-to-the-approved-submission"></a>在批准的提交中添加新的营销名称

检查已设置的发布日期。 如果发布日期已过，将无法添加新的名称。

### <a name="sharing-a-link-to-a-windows-certification-verification-report"></a>共享 Windows 认证验证报告的链接

* 可共享 URL 包含三个由斜杠分隔的标识号，如下所示：`https://developer.microsoft.com/dashboard/hardware/driver/DownloadCertificationReport/SellerID/PrivateProductID/SubmissionID`

* URL 中使用的标识号及其位置如下所示：

| 组件 | 说明 |
| ---       | ---         |
|SellerID   | 合作伙伴帐户的标识号。 可以在帐户管理页上的**帐户设置**下，找到该标识号。 |
|PrivateProductID | 每次创建产品时生成的标识号。 位于产品的驱动程序详细信息页上。 请参阅[仪表板 ID 定义](https://docs.microsoft.com/windows-hardware/drivers/dashboard/id-definitions)，了解详细信息。 |
|SubmissionID | 指定给每个提交和提交更新的标识号。 位于产品的驱动程序详细信息页上。 请参阅[仪表板 ID 定义](https://docs.microsoft.com/windows-hardware/drivers/dashboard/id-definitions)，了解详细信息。 |

* 若要创建可共享链接，请将以上示例 URL 中的 **SellerID**、**PrivateProductID** 和 **SubmissionID** 替换为相应的标识号。
* 无需事先获得授权或合作伙伴中心的访问权限，便可通过此 URL 访问并下载报告。

## <a name="troubleshooting-submission-upload-errors"></a>解决提交上传错误

### <a name="my-driver-signing-submission-fails-with-the-error-there-are-files-at-the-root-of-the-cabinet-or-no-inf-files-found-in-driver-directorydirectories-xyz"></a>驱动程序签名提交失败，并显示错误“在 Cabinet 根处有文件”或者“在以下驱动程序目录中找到了 \#No 个 .inf 文件：XYZ”

失败是由 .cab 文件的结构错误导致。 .cab 结构是使用 .cab 文件的根文件夹中的驱动程序文件创建，而非将它们置于子文件夹中。 有关如何为驱动程序签名提交创建正确的 .cab 文件的说明，请参阅[对内核驱动程序进行证明签名以便公开发布](attestation-signing-a-kernel-driver-for-public-release.md)。

### <a name="it-looks-like-your-package-is-corrupt-or-missing-important-information-ensure-you-are-using-the-latest-version-of-the-kit-regenerate-your-package-and-try-again-if-you-continue-to-experience-the-issue-contact-support"></a>“似乎程序包已损坏或丢失了重要信息。 请确保使用最新版本的工具包，重新生成程序包，然后再试一次。 如果仍遇到问题，请联系支持人员。”

如果仍遇到程序包提交问题，请与仪表板标头中所列的支持人员联系。

### <a name="file-is-using-zip644gbfile-size"></a>“文件使用的是 Zip64 (文件大小超过 4GB)”

当上传的存档文件类型为 .zip64 而不是 .zip 时，会导致发生该错误。 这由文件大小较大导致。 若要修复该错误，请按照以下步骤操作重新打包提交。

1. 将当前的 .hckx/hlkx 文件重命名为 .zip。
2. 解压缩到某个文件夹。
3. 打开该文件夹。
4. 选择所有项目，然后选择并按住（或右键单击）并选择“发送到压缩 zip 文件夹”。
5. 将新的 .zip 文件夹重命名为 .hckx/.hlkx。
6. 上载新的 .hckx/.hlkx 文件。

### <a name="the-dua-package-error-shows-failed-to-open-package-with-the-error-not-compatible-with-a-version-3200-with-this-instance-package-manager"></a>DUA 程序包错误显示“无法打开程序包”，带有错误“与包含此实例程序包管理器的版本 (3.2.0.0) 不兼容”

* 使用 [HLK Studio](https://docs.microsoft.com/windows-hardware/test/hlk/user/install-standalone-hlk-studio) 来打开下载的 DUA shell 程序包，并创建 DUA 提交。
