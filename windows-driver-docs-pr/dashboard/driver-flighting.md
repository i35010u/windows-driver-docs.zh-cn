---
title: 驱动程序外部测试
description: 合作伙伴中心中的驱动程序外部测试使你能够在定义的 Windows 预览体验成员圈中分发驱动程序，并提供自动监视和评估。
ms.date: 07/27/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: a6cf66d1d57bc66da2f732db121470f17240709b
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "63335116"
---
# <a name="driver-flighting"></a>驱动程序外部测试

合作伙伴中心中的驱动程序外部测试使你能够在定义的 Windows 预览体验成员圈中分发驱动程序，同时提供自动监视和评估。 完成外部测试后，将会生成一份驱动程序性能报告，使你能够评估其关键功能和更新方案。 成功完成外部测试并获得 Microsoft 批准后，该驱动程序即可通过 Windows 更新公开分发。 

以下视频更详细地概述了驱动程序外部测试计划： 
<iframe src="https://channel9.msdn.com/Events/WinHEC/WinHEC-Online/Start-Your-Driver-Flighting-The-benefit-of-Driver-Promotion/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="signing-up-for-driver-flighting"></a>注册驱动程序外部测试

若要注册驱动程序外部测试，请向合作伙伴中心提交一个支持票证。 可以在浏览器窗口的右上角访问合作伙伴中心支持，如下所示：

![用于访问合作伙伴中心支持的按钮](images/support.jpg)

> [!NOTE]
> 在注册驱动程序外部测试时，请确保处于合作伙伴中心内。 如果单击合作伙伴中心的其他区域中的支持按钮，则会为你联系非仪表板支持组。

在票证内，指定以下内容：

- 驱动程序要面向的现有设备的估计数量
- 每月将提出的推广请求的估计数量
- 卖家和/或发布者 ID

收到你的支持票证后，最长可能需要 5 个工作日你便可收到回复。

帐户获批后，组织管理员将能够通过转至**设置**页并选择**管理用户**来配置用户以进行外部测试。 请确保相应的用户具有至少一个以下选定的角色：

- 发货标签所有者
- 发货标签推广者

## <a name="how-to-promote-a-driver-for-driver-flighting"></a>如何推广驱动程序以进行驱动程序外部测试

在将驱动程序提交到合作伙伴中心后，可以使用以下步骤推广驱动程序以进行外部测试：

1. 驱动程序提交并且处于处理的**验证**阶段后，请创建新的发货标签并填写“详细信息”  和“属性”  部分。 有关详细信息，请参阅[将驱动程序发布到 Windows 更新](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)。

2. 按照如下所述，选择一个或多个驱动程序推广选项，以推广驱动程序进行外部测试：

|                            推广选项                             |                                                               说明                                                                |
|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
|   在 Windows 升级期间自动交付和安装驱动程序   | 标记驱动程序以通过动态更新交付，使其在操作系统升级期间交付至适用的计算机。 |
| 在所有适用的系统上自动交付和安装驱动程序。 |                将驱动程序标记为关键更新 (CU)，使其通过 Windows 更新自动安装。                 |

3. 填写外部测试推广所需的其他详细信息：
    1. 与你合作进行推广的 Microsoft 赞助商的电子邮件地址
    2. 推广发布请求的业务理由
    3. 用于验证驱动程序质量的流程
    4. 受驱动程序发布影响的 OEM（如有）

4. 选择适用于你的驱动程序的适当声明。 这些答案将提高评估流程的速度：![一个显示了可能适用于正进行外部测试的驱动程序的声明的图像：这是一个联合研发的驱动程序，需要重新启动，用于部署 UI 和/或软件。它支持新的或未发布的设备](images/driver-flighting-statements.png)

    > [!IMPORTANT] 
    > 请注意以下事项：
    > * 建议避免在安装驱动程序之后要求重新启动。 
    > * 处于 S 模式的 Windows 10 不支持在驱动程序安装过程中部署 UI 和/或软件，并且无法针对此操作系统进行外部测试。
    > * 联合研发的驱动程序是为未发布版本的 Windows 开发的驱动程序。 联合研发的驱动程序： 
    >    * 将在外部测试过程中仅分发给 Microsoft 预览体验计划中适用的设备。
    >    * 成功完成外部测试之后也不会分发给 Microsoft 预览体验计划之外的设备。
    >    * 将在 60 天后终止用于外部测试。 完成外部测试流程后，将提供外部测试版 bug 报告。 

5. 像往常一样完成发货标签流程。

推广驱动程序以发货后，Microsoft 将会评估你的驱动程序以等待审批，并在评估完成后提供驱动程序外部测试报告 - 一般会在发货标签发布后的两周内提供。 请注意，如果重复使用先前创建的发货标签，则不会更新其发布日期。

## <a name="reasons-a-driver-may-be-rejected"></a>驱动程序可能会被拒绝的原因

驱动程序遭拒有多种原因。 通常情况下，驱动程序遭拒是因驱动程序定位不当所致。 其中包括：

- 既面向先前版本的 Windows，同时也面向 Windows 10。
- 所面向的设备类可能具有你未能正确遵循的特定 CHID 面向要求。  某些设备类需要 CHID（如固件），其他类会禁止使用 CHID（如屏幕）。  请确保已正确输入你的信息。
- 使用的硬件 ID 无意中面向其他 OEM。

## <a name="related-topics"></a>相关主题

- [创建新的硬件提交](create-a-new-hardware-submission.md)
- [在合作伙伴中心内管理硬件提交](manage-your-hardware-submissions.md)
- [获取由 Microsoft 签名的适用于多个 Windows 版本的驱动程序](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
