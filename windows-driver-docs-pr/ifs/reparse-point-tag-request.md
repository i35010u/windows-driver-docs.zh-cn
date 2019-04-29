---
title: 重新分析点标记请求
description: 这是若要获取的重新分析点标记，需要一个这些文件系统筛选器驱动程序的机制。
ms.assetid: B4E4382B-4FB8-4E21-8FC4-EDDE8DD4AC77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ed9aa4f44f08bd41a64588d5f8350074dfc2b7f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370109"
---
# <a name="reparse-point-tag-request"></a>重新分析点标记请求


这是若要获取的重新分析点标记，需要一个这些文件系统筛选器驱动程序的机制。

## <a name="span-idreparsepointtagrequestspanspan-idreparsepointtagrequestspanspan-idreparsepointtagrequestspanreparse-point-tag-request"></a><span id="Reparse_Point_Tag_Request"></span><span id="reparse_point_tag_request"></span><span id="REPARSE_POINT_TAG_REQUEST"></span>重新分析点标记请求


若要获取的重新分析点标记，请向 Microsoft 发送以下信息。

-   公司名称
-   公司电子邮件
-   公司 URL
-   联系人电子邮件
-   产品名称
-   产品 URL
-   产品描述：（1 段落摘要）
-   驱动程序文件名
-   驱动程序设备名称
-   驱动程序的 GUID
-   高延迟位启用 （是/否）
-   名称的代理项位启用 （是/否）

将此信息发送到以 ASCII 文本电子邮件<rpid@microsoft.com>。 一个*ReparseID*此驱动程序将通过电子邮件发送回指定联系人的电子邮件地址的值。

以下列表详细介绍了一些要求提交请求。

- 必须填写所有字段。

- 对于那些不希望在此可公开查看数据库中使用其自己的姓名和电子邮件地址，创建为此，请使用电子邮件地址 （对于其他公司将包括文件系统/筛选器驱动程序的产品，具有互操作性问题同样的问题，并需要获取两个公司相互通信的测试/开发团队）。 建议的名称是 *"ntifskit@YourCompanyName.com"*。

- 如果启用了"高延迟"位，这意味着，驱动程序标记文件，并应能够长时间延迟。 例如，这将由驱动程序的使用重新分析点来实现块存储解决方案等设置。

- 如果启用"代理项名称"位，这意味着该驱动程序表示系统中的另一个命名的实体。 例如，或一个目录接合点的卷装入点的名称。

- 重新分析点是一项强大功能的 Windows，但开发人员应注意，只能有一个重新分析点，每个文件，并且某些 Windows 机制使用重新分析点 （HSM，本机结构化存储）。 开发人员需要具有重分析点标记已被使用的文件中时的回退策略。

 

 




