---
Description: 对于对象的要求
title: 对于对象的要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ae8f6f73b76d70aac555b1d197dfa6f3dbec8f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376226"
---
# <a name="requirements-for-objects"></a>对于对象的要求


Windows 便携式设备 (WPD) 进行分类内容类型的所有的对象。 特定类型的对象应支持最小列表的属性和资源 （和，对于设备对象，一系列命令）。 描述对象的类型及其[WPD\_对象\_内容\_类型](https://msdn.microsoft.com/library/windows/hardware/ff597893#wpd-object-content-type)属性; 每个对象必须支持此属性。

WPD 定义以下内容类型 （作为 GUID 值）。 供应商可以通过提供其自己的 GUID 创建其自己的自定义内容类型。

请注意常规用途的应用程序通常只处理一个预定义的类型。 供应商应用程序可以充分利用他们知道的自定义类型。

每个对象类型的属性和资源，必须支持，请参阅下表中的对象类型的每个说明页。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">内容类型 GUID</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597834" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_ALL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597834)"><strong>WPD_CONTENT_TYPE_ALL</strong></a></td>
<td align="left">此内容类型才有效使用中的某些查询方法来指示你感兴趣的所有设备类型;无法创建此类型的对象。
<p>如果您正在设计的自定义对象，它必须支持这些属性，最小值。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597835" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_APPOINTMENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597835)"><strong>WPD_CONTENT_TYPE_APPOINTMENT</strong></a></td>
<td align="left">对象是在一个日历约会。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597836" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_AUDIO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597836)"><strong>WPD_CONTENT_TYPE_AUDIO</strong></a></td>
<td align="left">对象是一个音频文件，例如 WMA 或 MP3 文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597837" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_AUDIO_ALBUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597837)"><strong>WPD_CONTENT_TYPE_AUDIO_ALBUM</strong></a></td>
<td align="left">对象是音频唱片集。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597838" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CALENDAR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597838)"><strong>WPD_CONTENT_TYPE_CALENDAR</strong></a></td>
<td align="left">对象是一个日历。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597839" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CERTIFICATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597839)"><strong>WPD_CONTENT_TYPE_CERTIFICATE</strong></a></td>
<td align="left">对象是用于身份验证的证书。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597840" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CONTACT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597840)"><strong>WPD_CONTENT_TYPE_CONTACT</strong></a></td>
<td align="left">对象是个人的联系人数据，如 vCard 文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597841" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CONTACT_GROUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597841)"><strong>WPD_CONTENT_TYPE_CONTACT_GROUP</strong></a></td>
<td align="left">对象表示一组联系人。 此对象的 WPD_OBJECT_REFERENCES 属性包含各种 WPD_CONTENT_TYPE_CONTACT 对象的对象标识符的列表。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597842" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_DOCUMENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597842)"><strong>WPD_CONTENT_TYPE_DOCUMENT</strong></a></td>
<td align="left">对象是使用或不带格式文本的容器。 示例包括 Microsoft Word 文件和纯文本文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597843" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_EMAIL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597843)"><strong>WPD_CONTENT_TYPE_EMAIL</strong></a></td>
<td align="left">对象是一封电子邮件。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597844" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_FOLDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597844)"><strong>WPD_CONTENT_TYPE_FOLDER</strong></a></td>
<td align="left">对象是一个文件夹。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597845" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_FUNCTIONAL_OBJECT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597845)"><strong>WPD_CONTENT_TYPE_FUNCTIONAL_OBJECT</strong></a></td>
<td align="left">对象是表示设备功能的功能对象。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597846" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_GENERIC_FILE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597846)"><strong>WPD_CONTENT_TYPE_GENERIC_FILE</strong></a></td>
<td align="left">对象是不属于任何其他预定义内容类型的文件的一般的物理文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597848" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_IMAGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597848)"><strong>WPD_CONTENT_TYPE_IMAGE</strong></a></td>
<td align="left">对象是一个静态的图像，如 JPEG 文件。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597849" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_IMAGE_ALBUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597849)"><strong>WPD_CONTENT_TYPE_IMAGE_ALBUM</strong></a></td>
<td align="left">对象是映像唱片集。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597851" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MEDIA_CAST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597851)"><strong>WPD_CONTENT_TYPE_MEDIA_CAST</strong></a></td>
<td align="left">对象是强制转换的媒体对象。 强制转换的媒体对象可以表示组相关的联机发布内容的容器对象。 例如，RSS 通道可以表示为强制转换的媒体对象，而此对象的 WPD_OBJECT_REFERENCES 属性包含的对象标识符表示通道中的每个项的列表。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597851" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MEMO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597851)"><strong>WPD_CONTENT_TYPE_MEMO</strong></a></td>
<td align="left">对象表示备注数据，例如，文本注释。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597852" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MIXED_CONTENT_ALBUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597852)"><strong>WPD_CONTENT_TYPE_MIXED_CONTENT_ALBUM</strong></a></td>
<td align="left">对象是混合媒体对象的唱片集 — 例如，音频、 图像和视频文件。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597854" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_PLAYLIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597854)"><strong>WPD_CONTENT_TYPE_PLAYLIST</strong></a></td>
<td align="left">对象是一个播放列表。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597855" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_PROGRAM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597855)"><strong>WPD_CONTENT_TYPE_PROGRAM</strong></a></td>
<td align="left">对象表示可以运行，例如，一个脚本或可执行文件的文件。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597856" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597856)"><strong>WPD_CONTENT_TYPE_SECTION</strong></a></td>
<td align="left">对象描述另一个对象中包含的数据的部分。 例如，最可能由一系列的章节描述较大的音频文件。 每一章可以是具有其自己的一章艺术作品、 元数据和等等，WPD_CONTENT_TYPE_SECTION 对象，并且其数据是大型的音频文件的子集 （例如，第一章是第一个 10 分钟，第二个章节都是在接下来的 20 分钟等等)。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597857" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_TASK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597857)"><strong>WPD_CONTENT_TYPE_TASK</strong></a></td>
<td align="left">对象是一个任务，例如待办事项列表中的项。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597858" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_TELEVISION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597858)"><strong>WPD_CONTENT_TYPE_TELEVISION</strong></a></td>
<td align="left">对象是电视节目录制内容。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597859" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_UNSPECIFIED&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597859)"><strong>WPD_CONTENT_TYPE_UNSPECIFIED</strong></a></td>
<td align="left">对象是不在预定义 WPD 内容类型的泛型对象。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597860" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_VIDEO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597860)"><strong>WPD_CONTENT_TYPE_VIDEO</strong></a></td>
<td align="left">对象是视频中的，如 WMV 或 AVI 文件。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597861" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_VIDEO_ALBUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597861)"><strong>WPD_CONTENT_TYPE_VIDEO_ALBUM</strong></a></td>
<td align="left">对象是视频的唱片集。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597862" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_WIRELESS_PROFILE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff597862)"><strong>WPD_CONTENT_TYPE_WIRELESS_PROFILE</strong></a></td>
<td align="left">对象包含无线网络访问权限信息。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff597563" data-raw-source="[Device Object](https://msdn.microsoft.com/library/windows/hardware/ff597563)">设备对象</a></td>
<td align="left">不<strong>PROPERTYKEY</strong>，但所有对象都必须都支持在本部分中列出的属性。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





