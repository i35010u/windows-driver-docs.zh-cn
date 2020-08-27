---
title: 微筛选器等级请求
description: 微筛选器等级请求
ms.assetid: 4861E5FC-9883-455F-A925-EBAFC890F568
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35459292f47e0e6284aab66993122d5bb510f250
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902530"
---
# <a name="minifilter-altitude-request"></a>微筛选器等级请求

开发到筛选器管理器模型的文件系统微筛选器驱动程序必须具有唯一的标识符，该标识符被称为定义其相对于文件系统堆栈中存在的其他 minifilters 的位置的高度。

若要请求微筛选器海拔标识符，请将 ASCII 文本电子邮件中的电子邮件发送到 [fsfcomm@microsoft.com](mailto:fsfcomm@microsoft.com?subject=Minifilter%20altitude%20request) 主题： "微筛选器限制请求"。 电子邮件的正文必须包含以下字段和相应信息。

然后，将通过电子邮件将此筛选器发回到指定的联系人电子邮件地址。

你还可以将电子邮件发送到 [fsfcomm@microsoft.com](mailto:fsfcomm@microsoft.com?subject=Minifilter%20altitude%20request) 以更新与现有高度关联的信息。

|字段|评论|
|----|----|
|公司名称：| |
|联系人电子邮件：|提供长期公司电子邮件别名，而不是单独的电子邮件。|
|产品名称：| |
|产品 URL：| |
|产品/筛选器描述：|一个段落摘要，可帮助 Microsoft 确定筛选器的适当高度。|
|筛选器文件名：| |
|滤波器类型：|以下值之一：注册表、FileSystem、Both|
|筛选启动类型：|以下值之一：启动、系统、自动、要求|
|请求的筛选器加载顺序组：|请参阅为可用的加载顺序组 [分配的文件系统微筛选](allocated-altitudes.md) 器。|
|请求海拔：|Microsoft 保留分配不同于所请求海拔高度的权限，具体取决于高度可用性和筛选器驱动程序功能。|
|其他信息：|使用此字段，告知我们在向此筛选器分配海拔时是否有任何要考虑的信息。|

下面是分配请求电子邮件正文的示例。

``` syntax
Hi,

Below is the request information to assign an altitude for our Contoso DataKleen file system minifilter.

Company name: Contoso Ltd.
Contact e-mail: filterdevgroup@contoso.com
Product name: Contoso DataKleen
Product URL: http://fsfilters.contoso.com
Product/Filter Description: The Contoso DataKleen filter removes all occurrences of any byte having a value between 128 and 255 during file reads. Our minifilter removes this value since it is not displayable on TTY devices.
Filter filename: ContosoDK.sys
Filter type: FileSystem
Filter start-type: Demand
Requested filter load order group: FSFilter Content Screener
Requested altitude: 268400
Additional information: None

Thanks,

FilterDev
```

>[!NOTE]
>- 必须填写所有字段。
>- 最多可能需要两周的时间来处理和分配高度。 缺少的任何信息可能会延迟分配。
>- 分配的海拔将最终反映在 " [文件系统微筛选](allocated-altitudes.md)器" 中列出的高度。 请注意，Microsoft 每年仅更新此列表。
