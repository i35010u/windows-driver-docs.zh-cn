---
title: 重新分析点标记请求
description: 描述如何获取需要一个重分析点标记的那些文件系统筛选器驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2261af8b8ff87889f5cdfb219fbca33043e48e77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798179"
---
# <a name="reparse-point-tag-request"></a>重新分析点标记请求

如果要开发的文件系统筛选器驱动程序需要重新分析点标记，请向发送 ASCII 文本电子邮件， <rpid@microsoft.com> 其中包含以下信息。

- 公司名称
- 公司电子邮件
- 公司 URL
- 联系人电子邮件
- 产品名称
- 产品 URL
- 产品说明： (1 段落摘要) 
- 驱动程序文件名
- 驱动程序设备名称
- 驱动程序 GUID
- 已启用高延迟位 (是/否) 
- 已启用名称代理项 (是/否) 

然后，会将此驱动程序的 *ReparseID* 值通过电子邮件发送回指定的联系人电子邮件地址。

以下列表详细说明了提交请求的一些要求。

- 必须填写所有字段。

- 对于不希望在此可公开查看的数据库中使用其自己的名称和电子邮件地址的用户，请为包含文件系统/筛选器驱动程序（具有与) 您的互操作性问题）的产品的其他公司 (创建一个电子邮件地址。 建议的名称为 *" ntifs@YourCompanyName.com "*。

- 如果启用 "高延迟" 位，这意味着驱动程序标记文件和预计会有较长的延迟。 例如，使用重新分析点实现分层存储解决方案等的驱动程序将设置此设置。

- 如果启用 "名称代理项" 位，这意味着该驱动程序表示系统中的另一个命名实体;例如，卷装入点或目录接合点的名称。

重新分析点是 Windows 的一项强大功能，但开发人员应注意每个文件只能有一个重新分析点，而某些 Windows 机制使用重新分析点 (HSM、本机结构化存储) 。 当重新分析点标记已用于某个文件时，开发人员需要提供回退策略。

有关重新 [分析点和重分析点标记](/windows/win32/fileio/reparse-points)的详细信息，请参阅 Windows SDK 文档。
