---
title: 提交桌面 COSA/APN 数据库更新
description: 提交桌面 COSA/APN 数据库更新
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1babd49c11f3503992533d1befb2fc18391662c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823039"
---
# <a name="submitting-the-desktop-cosaapn-database-update"></a>提交桌面 COSA/APN 数据库更新

>[!IMPORTANT]
> 以下提交接入点更新的步骤适用于桌面 COSA （用于 Windows 10 版本1703及更高版本）和 apndatabase.xml，适用于1703之前的 windows 8、Windows 8.1 和版本。 如果你面向的是 Windows 10 1703 版或更高版本，则 Microsoft 会将 apndatabase.xml 提交转换为 COSA。

现在，你已测试了 APN 条目，现在可以按照本主题中的步骤将其提交给 Microsoft。

## <a name="fill-out-the-apn-testing-questionnaire"></a>填写 APN 测试调查表

测试接入点值后，必须填写以下调查表。 这会在你提交的过程中发送到 TAM。

此调查表旨在确保你已完成测试并帮助 Microsoft 团队了解你测试传入 APNs 的程度。

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

## <a name="submit-cosaapn-database-updates-to-microsoft"></a>向 Microsoft 提交 COSA/APN 数据库更新

使用以下过程将 COSA 或 APN 连接数据库更新提交给 Microsoft。 

1.  **请与 MICROSOFT TAM 联系** ，使用 [测试桌面 COSA/APN 数据库提交](testing-your-desktop-cosa-apn-database-submission.md)中所述的相同 MS 解决案例，为你的 tam 提供已完成的接入点测试调查表，以描述已完成的测试级别。  

2.  **Microsoft 会审过程** -microsoft 将查看你的提交内容，如果检测到错误，可能会与你联系。 Microsoft 不会对你的移动网络进行任何测试。 如果提交时未检测到任何错误，则会在发布过程中进行。

3.  **操作员验证** --由于 Microsoft 无法测试为你的移动网络提供的 APNs，因此在生成新的 COSA 预配包或 APN 数据库后，将要求你执行此操作。 系统将提供 COSA 文件或 APN 数据库 XML 文件的新副本，你可以将其应用于电脑并在实际网络上测试该功能。 你将进行另一次测试，如 [测试桌面 COSA/APN 数据库提交](testing-your-desktop-cosa-apn-database-submission.md)中所述。 Microsoft TAM 将为你提供一个可安装文件，该文件将使用更新的数据库对电脑上的 COSA 或 APN 数据库进行修补。 系统会提供一个特定时间段来测试新的 APN 数据库。 完成测试后，将要求你使用你的注册回复你的 Microsoft 联系人。 如果遇到问题或错误，可能有有限的机会来更正此问题。 如果无法及时更正此问题，则将从 APN 数据库的下一个已发布更新中恢复你所做的更改。 需要重新提交 APN 连接数据库提交，并等待到下一个计划的更新。 

4.  **更新已发布** --在新的 APN 数据库上注销后，将完成更新发布过程。 准备就绪后，它将显示在 Windows 更新供用户安装。 完成 APN 数据库提交后，将提供更详细的发布时间线。

> [!IMPORTANT]
> 如果在分配的时间段内未注销，你的更改将从 APN 连接数据库的下一次发布更新中恢复。 需要重新提交接入点提交，并等待下一个计划的更新。   

### <a name="deleting-an-apn-database-entry"></a>删除 APN 数据库条目

删除 APN 条目被视为一种特殊的操作。 如果仅删除某个条目，则无需填写电子表格。 通过回答以下调查表，列出要删除的 APN 连接数据库中的条目。 完成此操作后，将其发送到 TAM。

> [!NOTE]
> 删除 **操作根据操作员** 和 **国家/地区** 组合进行。 

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





