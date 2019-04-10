---
title: 微筛选器等级请求
description: 微筛选器等级请求
ms.assetid: 4861E5FC-9883-455F-A925-EBAFC890F568
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 310b6abb180422126f89f0cdb9a27d946f2fd047
ms.sourcegitcommit: 58d5457779071709faab68e44decc3c48a2cf975
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59362913"
---
# <a name="minifilter-altitude-request"></a>微筛选器等级请求

文件系统微筛选器驱动程序开发到筛选器管理器模型必须具有名为海拔高度，用于定义其位置相对于存在于文件系统堆栈中其他微筛选器的唯一标识符。

若要请求微筛选器海拔高度标识符，对 ASCII 文本电子邮件中发送电子邮件[ fsfcomm@microsoft.com ](mailto:fsfcomm@microsoft.com?subject=Minifilter%20altitude%20request)与该主题："微筛选器海拔高度请求"。 电子邮件的正文必须包含以下字段和相应的信息。

然后，此筛选器的海拔高度将通过电子邮件发送回指定联系人的电子邮件地址。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">公司名称：</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">联系人电子邮件：</td>
<td align="left">提供长期公司电子邮件别名，而不是个人电子邮件。</td>
</tr>
<tr class="odd">
<td align="left">产品名称：</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">产品 URL:</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">产品/筛选器说明：</td>
<td align="left">一个段落摘要，帮助 Microsoft 确定适当的海拔高度的筛选器。</td>
</tr>
<tr class="even">
<td align="left">筛选器文件名：</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">筛选器类型：</td>
<td align="left">下列值之一：注册表、 文件系统，同时</td>
</tr>
<tr class="even">
<td align="left">启动类型的筛选器：</td>
<td align="left">下列值之一：启动、 系统、 自动需求</td>
</tr>
<tr class="odd">
<td align="left">请求的筛选器加载顺序组：</td>
<td align="left">请参阅<a href="allocated-altitudes.md" data-raw-source="[File System Minifilter Allocated Altitudes](allocated-altitudes.md)">文件系统微筛选器分配海拔地区</a>为可用的加载顺序组。</td>
</tr>
<tr class="even">
<td align="left">请求的海拔高度：</td>
<td align="left">Microsoft 保留权分配不同于请求海拔高度，具体取决于海拔高度可用性和筛选器驱动程序功能海拔高度。</td>
</tr>
<tr class="odd">
<td align="left">其他信息：</td>
<td align="left">使用此字段，让我们知道是否有你想 Microsoft 将海拔高度分配给此筛选器时要考虑的任何信息。</td>
</tr>
</tbody>
</table>

下面是一个示例，用于分配请求电子邮件的正文。

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

## <a name="note"></a>注意

* 必须填写所有字段。
* 它可能需要 Microsoft 到两周，以处理并分配海拔的地区。 任何缺少的信息可能会延迟赋值。
* 已分配的海拔高度最终会反映在海拔中列出的地区[文件系统微筛选器分配海拔地区](allocated-altitudes.md)。 请注意，Microsoft 仅更新此列表每年一次。