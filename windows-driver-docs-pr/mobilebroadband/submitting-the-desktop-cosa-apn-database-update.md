---
title: 提交桌面 COSA/APN 数据库更新
description: 提交桌面 COSA/APN 数据库更新
ms.assetid: 1ad1be32-74c9-4f84-b680-9124135a3b66
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4cf888a4abc2778022132a3e7962ee2f0307144
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376634"
---
# <a name="submitting-the-desktop-cosaapn-database-update"></a>提交桌面 COSA/APN 数据库更新

>[!IMPORTANT]
> 以下步骤以提交 APN 更新适用于 Windows 10，版本 1703年及更高版本，和 apndatabase.xml，用于 Windows 8、 Windows 8.1 和 Windows 10 版本 1703年之前使用这两个桌面 COSA。 如果你面向 Windows 10 版本 1703年或更高版本，Microsoft 会将转换到 COSA apndatabase.xml 提交。

现在，你已在测试 APN 条目，就现在可以按照本主题中的步骤将其提交到 Microsoft。

## <a name="fill-out-the-apn-testing-questionnaire"></a>填写 APN 测试调查表

测试你的 APN 值后, 必须填写以下调查表。 这将发送到您的 TAM 作为你的提交内容的一部分。

本问卷的目的是确保您已完成测试并帮助 microsoft 团队，了解如何全面测试传入 APNs。

```syntax
Please describe what testing you have done on the APNs that you are submitting.
   [describe here]

Have you tested these APN values on your network? Windows cannot test these APNs for you because we do not have access to your wireless network.
   [yes/no]

Do you understand that all the APNs that match the Operator and Country/Region combination will be wiped out and replaced by the APNs that you have attached to this request?
   [yes/no]

Have you attached an Excel sheet to this request?
   [yes/no]

Do you certify that you are entitled to submit an update on behalf of this operator?
   [yes/no]

Provide your contact information:
   [Name]
   [Company]
   [Job title]
   [E-mail from a corporate e- account for the company you are submitting for]
   [phone 1]
   [phone 2]
```

## <a name="submit-cosaapn-database-updates-to-microsoft"></a>提交给 Microsoft 的 COSA/APN 数据库更新

使用以下过程将 COSA 或 APN 连接数据库更新提交到 Microsoft。 

1.  **联系 Microsoft 客户 TAM** -使用相同的 MS 求解用例中所述[测试你的桌面 COSA/APN 数据库提交](testing-your-desktop-cosa-apn-database-submission.md)，向您的 TAM 提供已完成的 APN 测试调查表来描述的测试级别这样做了。  

2.  **Microsoft 会审过程**-Microsoft 将审查你的提交内容，可能会与你联系如果检测到错误。 Microsoft 不会做任何移动网络上进行测试。 如果你的提交中检测不到任何错误，它将继续通过发布过程。

3.  **运算符验证**-由于 Microsoft 无法测试的 APNs 移动网络提供，你将需要执行此操作后新 COSA 预配包或已生成 APN 数据库。 你将获得一份新 COSA.ppkg 文件或将使用适用于您的 Pc 并测试实际网络上的功能的 APN 数据库 XML 文件。 您将经历另一个测试通过，如中所述[测试您的桌面 COSA/APN 数据库提交](testing-your-desktop-cosa-apn-database-submission.md)。 Microsoft TAM 提供将 patch COSA 或已更新的数据库在 PC 上的 APN 数据库可安装文件。 将为您提供的特定时间段来测试新的 APN 数据库。 完成测试后，系统将要求要回复的签字认可的 Microsoft 联系人。 如果您发现问题或错误，可能有一个有限的机会来更正它。 如果不能及时纠正该问题，则会从 APN 数据库发布的下一步更新还原所做的更改。 你将需要重新提交你的 APN 连接数据库提交并等待，直到下一次计划更新。 

4.  **发布更新**-一旦您已签名对新的 APN 数据库，它将经历发布过程的更新。 准备就绪后，它将出现在要安装用户的 Windows 更新。 将为您提供更详细的发布时间线完成你的 APN 数据库提交后。

> [!IMPORTANT]
> 如果您做不注销分配的时间段内，则将从 APN 连接数据库发布的下一步更新还原所做的更改。 你将需要重新提交你的 APN 提交并等待，直到下一次计划更新。   

### <a name="deleting-an-apn-database-entry"></a>正在删除 APN 数据库条目

删除 APN 条目被视为特殊处理操作。 如果要仅删除一个条目，您无需填写电子表格。 列出你想要通过回答以下调查表已删除的 APN 连接数据库中的条目。 完成此操作后，将其发送到您的 TAM。

> [!NOTE]
> 删除操作发生时根据**运算符**并**国家/地区**组合。 

```syntax
Please describe which operator and region combination you wish to have removed from the APN database.
   [Describe here. For example: <Operator name="Contoso (Argentina)">]

Do you understand that all the APNs that match the Operator and Country/Region combination will be wiped out?
   [yes/no]

If you wish to add values to the APN database in addition to this deletion request, have you attached an Excel sheet and questionnaire for that add request?
   [not applicable/yes/no]

Do you certify that you are entitled to submit an update on behalf of this operator?
   [yes/no]

Provide your contact information:
   [Name]
   [Company]
   [Job title]
   [E-mail from a corporate email account for the company you are submitting for]
   [phone 1]
   [phone 2]
``` 





