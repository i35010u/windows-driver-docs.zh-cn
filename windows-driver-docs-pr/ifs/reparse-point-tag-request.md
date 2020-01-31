---
title: 重新分析点标记请求
description: 这是为需要重新分析点标记的那些文件系统筛选器提供程序的机制。
ms.assetid: B4E4382B-4FB8-4E21-8FC4-EDDE8DD4AC77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 229d74ba266c22da7369ad5eef5c39764b5c7e0d
ms.sourcegitcommit: 6997fcbd0ad57e189c4b7c6b490632d1d53b6b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822817"
---
# <a name="reparse-point-tag-request"></a>重新分析点标记请求


这是为需要重新分析点标记的那些文件系统筛选器提供程序的机制。

## <a name="span-idreparse_point_tag_requestspanspan-idreparse_point_tag_requestspanspan-idreparse_point_tag_requestspanreparse-point-tag-request"></a><span id="Reparse_Point_Tag_Request"></span><span id="reparse_point_tag_request"></span><span id="REPARSE_POINT_TAG_REQUEST"></span>重分析点标记请求


若要获取重新分析点标记，请将以下信息发送给 Microsoft。

-   公司名称
-   公司电子邮件
-   公司 URL
-   联系人电子邮件
-   产品名称
-   产品 URL
-   产品说明：（1段摘要）
-   驱动程序文件名
-   驱动程序设备名称
-   驱动程序 GUID
-   已启用高延迟位（是/否）
-   已启用名称代理项位（是/否）

将此信息以 ASCII 文本电子邮件消息发送到 <rpid@microsoft.com>。 然后，会将此驱动程序的*ReparseID*值通过电子邮件发送回指定的联系人电子邮件地址。

以下列表详细说明了提交请求的一些要求。

- 必须填写所有字段。

- 对于不希望在此可公开查看的数据库中使用其自己的名称和电子邮件地址的用户，请为此用途创建一个电子邮件地址（对于具有包含文件系统/筛选器驱动程序的产品的其他公司，它们具有互操作性问题，并且需要使两家公司的测试/开发团队相互通信）。 建议的名称为 *"ntifskit@YourCompanyName.com"* 。

- 如果启用 "高延迟" 位，这意味着驱动程序标记文件和预计会有较长的延迟。 例如，使用重新分析点实现分层存储解决方案等的驱动程序将设置此设置。

- 如果启用 "名称代理项" 位，这意味着该驱动程序表示系统中的另一个命名实体。 例如，卷装入点或目录接合点的名称。

- 重新分析点是 Windows 的一项强大功能，但开发人员应该知道每个文件只能有一个重新分析点，而某些 Windows 机制则使用重新分析点（HSM、本机结构化存储）。 当重新分析点标记已用于某个文件时，开发人员需要提供回退策略。

 

 




