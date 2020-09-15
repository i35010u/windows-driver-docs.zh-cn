---
description: 对于对象的要求
title: 对于对象的要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2a41cc6fb4f5fb32d3acde44a0b6e3db4b3d5d1
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101560"
---
# <a name="requirements-for-objects"></a>对于对象的要求


Windows 便携式设备 (WPD) 按内容类型对所有对象进行分类。 特定类型的对象应支持 (的属性和资源的最小列表，并为设备对象) 一组命令。 对象的类型由其 [WPD \_ 对象 \_ 内容 \_ 类型](/previous-versions/windows/hardware/drivers/ff597893(v=vs.85)#wpd-object-content-type) 属性描述; 每个对象都必须支持此属性。

WPD 定义 (为) GUID 值的以下内容类型。 供应商可以通过提供自己的 GUID 来创建自己的自定义内容类型。

注意一般用途的应用程序通常仅处理预定义的类型之一。 供应商应用程序可以充分利用他们知道的自定义类型。

若要了解每个对象类型必须支持的属性和资源，请参阅下表中每个对象类型的 "说明" 页。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">内容类型 GUID</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597834(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_ALL&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597834(v=vs.85))"><strong>WPD_CONTENT_TYPE_ALL</strong></a></td>
<td align="left">此内容类型仅在某些查询方法中用于指示你对所有设备类型感兴趣时才有效：不能创建这种类型的对象。
<p>如果要设计自定义对象，它至少必须支持这些属性。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597835(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_APPOINTMENT&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597835(v=vs.85))"><strong>WPD_CONTENT_TYPE_APPOINTMENT</strong></a></td>
<td align="left">对象是日历中的一个约会。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597836(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_AUDIO&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597836(v=vs.85))"><strong>WPD_CONTENT_TYPE_AUDIO</strong></a></td>
<td align="left">对象是一个音频文件，如 WMA 或 MP3 文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597837(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_AUDIO_ALBUM&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597837(v=vs.85))"><strong>WPD_CONTENT_TYPE_AUDIO_ALBUM</strong></a></td>
<td align="left">对象是一个音频唱片集。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597838(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CALENDAR&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597838(v=vs.85))"><strong>WPD_CONTENT_TYPE_CALENDAR</strong></a></td>
<td align="left">对象是一个日历。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597839(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CERTIFICATE&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597839(v=vs.85))"><strong>WPD_CONTENT_TYPE_CERTIFICATE</strong></a></td>
<td align="left">对象是用于身份验证的证书。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597840(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CONTACT&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597840(v=vs.85))"><strong>WPD_CONTENT_TYPE_CONTACT</strong></a></td>
<td align="left">对象是个人联系人数据，如 vCard 文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597841(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CONTACT_GROUP&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597841(v=vs.85))"><strong>WPD_CONTENT_TYPE_CONTACT_GROUP</strong></a></td>
<td align="left">对象表示一组联系人。 此对象的 WPD_OBJECT_REFERENCES 属性包含各种 WPD_CONTENT_TYPE_CONTACT 对象的对象标识符列表。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597842(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_DOCUMENT&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597842(v=vs.85))"><strong>WPD_CONTENT_TYPE_DOCUMENT</strong></a></td>
<td align="left">对象是带有或不带格式的文本的容器。 示例包括 Microsoft Word 文件和纯文本文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597843(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_EMAIL&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597843(v=vs.85))"><strong>WPD_CONTENT_TYPE_EMAIL</strong></a></td>
<td align="left">对象是一封电子邮件。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597844(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_FOLDER&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597844(v=vs.85))"><strong>WPD_CONTENT_TYPE_FOLDER</strong></a></td>
<td align="left">对象是一个文件夹。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597845(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_FUNCTIONAL_OBJECT&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597845(v=vs.85))"><strong>WPD_CONTENT_TYPE_FUNCTIONAL_OBJECT</strong></a></td>
<td align="left">对象是表示设备功能的函数对象。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597846(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_GENERIC_FILE&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597846(v=vs.85))"><strong>WPD_CONTENT_TYPE_GENERIC_FILE</strong></a></td>
<td align="left">对象是一般的物理文件，它不属于任何其他预定义的文件内容类型。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597848(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_IMAGE&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597848(v=vs.85))"><strong>WPD_CONTENT_TYPE_IMAGE</strong></a></td>
<td align="left">对象是静止图像，如 JPEG 文件。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597849(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_IMAGE_ALBUM&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597849(v=vs.85))"><strong>WPD_CONTENT_TYPE_IMAGE_ALBUM</strong></a></td>
<td align="left">对象是一个图像唱片集。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597851(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MEDIA_CAST&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597851(v=vs.85))"><strong>WPD_CONTENT_TYPE_MEDIA_CAST</strong></a></td>
<td align="left">对象是一个媒体转换对象。 媒体转换对象可以表示一个容器对象，用于对联机发布的相关内容进行分组。 例如，可以将 RSS 通道表示为 media cast 对象，此对象的 WPD_OBJECT_REFERENCES 属性包含一个对象标识符列表，该列表表示通道中的每一项。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597851(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MEMO&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597851(v=vs.85))"><strong>WPD_CONTENT_TYPE_MEMO</strong></a></td>
<td align="left">对象表示备注数据，例如文本注释。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597852(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MIXED_CONTENT_ALBUM&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597852(v=vs.85))"><strong>WPD_CONTENT_TYPE_MIXED_CONTENT_ALBUM</strong></a></td>
<td align="left">对象是混合媒体对象的唱片集，例如音频、图像和视频文件。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597854(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_PLAYLIST&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597854(v=vs.85))"><strong>WPD_CONTENT_TYPE_PLAYLIST</strong></a></td>
<td align="left">对象为播放列表。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597855(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_PROGRAM&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597855(v=vs.85))"><strong>WPD_CONTENT_TYPE_PROGRAM</strong></a></td>
<td align="left">对象表示可以运行的文件，例如脚本或可执行文件。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597856(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_SECTION&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597856(v=vs.85))"><strong>WPD_CONTENT_TYPE_SECTION</strong></a></td>
<td align="left">对象描述包含在另一个对象中的数据部分。 例如，大型音频文件可能最好由一系列章节描述。 每一章都可以是一个 WPD_CONTENT_TYPE_SECTION 对象，它具有自己的章节艺术、元数据等，并且其数据是大型音频文件的子集 (例如，第一章是前10分钟，第二章是在) 时。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597857(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_TASK&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597857(v=vs.85))"><strong>WPD_CONTENT_TYPE_TASK</strong></a></td>
<td align="left">对象是任务，如待办事项列表中的项。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597858(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_TELEVISION&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597858(v=vs.85))"><strong>WPD_CONTENT_TYPE_TELEVISION</strong></a></td>
<td align="left">对象是电视节目。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597859(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_UNSPECIFIED&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597859(v=vs.85))"><strong>WPD_CONTENT_TYPE_UNSPECIFIED</strong></a></td>
<td align="left">对象是不属于预定义 WPD 内容类型的泛型对象。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597860(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_VIDEO&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597860(v=vs.85))"><strong>WPD_CONTENT_TYPE_VIDEO</strong></a></td>
<td align="left">对象是视频，例如 WMV 或 AVI 文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597861(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_VIDEO_ALBUM&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597861(v=vs.85))"><strong>WPD_CONTENT_TYPE_VIDEO_ALBUM</strong></a></td>
<td align="left">对象是视频唱片集。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597862(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_WIRELESS_PROFILE&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff597862(v=vs.85))"><strong>WPD_CONTENT_TYPE_WIRELESS_PROFILE</strong></a></td>
<td align="left">对象包含无线网络访问信息。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/windows/hardware/drivers/ff597563(v=vs.85)" data-raw-source="[Device Object](/previous-versions/windows/hardware/drivers/ff597563(v=vs.85))">设备对象</a></td>
<td align="left">不是 <strong>PROPERTYKEY</strong>，但是所有对象都必须支持本节中列出的属性。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

