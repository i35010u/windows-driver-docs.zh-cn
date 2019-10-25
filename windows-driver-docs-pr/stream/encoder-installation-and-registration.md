---
title: 编码器安装和注册
description: 编码器安装和注册
ms.assetid: 6ce0c504-977a-4db5-b5ee-128b69ce8eba
keywords:
- 内核流式处理类别 WDK 编码器
- 编码器设备 WDK AVStream
- AVStream WDK，编码器设备
- 未压缩的数据流 WDK AVStream
- 编码流 WDK AVStream
- 音频编码器设备 WDK AVStream
- 视频编码器设备 WDK AVStream
- INF 文件 WDK 编码器
- 元数据 WDK 编码器
- KS 代理 WDK AVStream
- 内核流式处理代理 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5542fd5b9fd72244ebdc491049391e33f1fdc6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834430"
---
# <a name="encoder-installation-and-registration"></a>编码器安装和注册


带有编码器筛选器的驱动程序的 INF 文件必须包含用于定义以下内容的条目：

-   其他内核流式处理捕获组件

-   应公开哪个 COM 接口 KsProxy

-   描述编码器筛选器功能的元数据值

-   筛选器的内核流式处理类别

### <a name="additional-kernel-streaming-capture-components"></a>**其他内核流式处理捕获组件**

用于安装编码器设备驱动程序的 INF 文件必须在其 \[DefaultInstall\] 部分中引用*ks*和*kscaptur* ，因为这些文件添加了必要的编码器组件支持。 例如：

```INF
[DefaultInstall]
include=ks.inf,kscaptur.inf
needs=[Your driver's DDInstall section],KS.Registration,KSCAPTUR.Registration.NT
```

### <a name="which-com-interface-ksproxy-should-expose"></a>**应公开哪个 COM 接口 KsProxy**

在驱动程序的 INF 文件的 " **AddReg** " 部分中，指定以下三个 guid 之一，以指示 KsProxy 插件（*encapi*）应向客户端公开的 COM 接口。 COM 接口由编码器筛选器中实现的属性支持确定：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>接口 GUID</th>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>{B43C4EEC-8C32-4791-9102-508ADA5EE8E7}</p></td>
<td><p><strong>CLSID_IVideoEncoderProxy</strong></p></td>
<td><p>指定此 GUID 将导致 KsProxy 公开<strong>IVideoEncoder</strong> COM 接口（以便向后兼容由 Microsoft 提供的早期版本的编码器支持）。 客户端必须从<strong>IEncoderAPI</strong> COM 接口派生此接口。</p></td>
</tr>
<tr class="even">
<td><p>{7FF0997A-1999-4286-A73C-622B8814E7EB}</p></td>
<td><p><strong>CLSID_ICodecAPIProxy</strong></p></td>
<td><p>指定此 GUID 将导致 KsProxy 公开<strong>ICodecAPI</strong> COM 接口（对于非视频编码设备，例如仅音频编码器）。</p></td>
</tr>
<tr class="odd">
<td><p>{B05DABD9-56E5-4FDC-AFA4-8A47E91F1C9C}</p></td>
<td><p><strong>CLSID_IVideoEncoderCodecAPIProxy</strong></p></td>
<td><p>指定此 GUID 可导致 KsProxy 同时公开<strong>IVideoEncoder</strong>和<strong>ICodecAPI</strong> COM 接口（对于向后和向前兼容性）。</p></td>
</tr>
</tbody>
</table>

 

例如：

```INF
[Your driver's AddReg section]
HKR,Interfaces\{B43C4EEC-8C32-4791-9102-508ADA5EE8E7},,,
```

这将导致 KsProxy 只公开**IVideoEncoder** （**CLSID\_IVideoEncoderProxy**） COM 接口。

这些 COM 接口记录在适用于 Windows XP SP1 和更高版本的 DirectX 9 和 Windows Sdk 的 DirectShow 部分中。

### <a href="" id="metadata-values-that-advertise-the-encoder-filter-s-capabilities"></a>**宣传编码器筛选器功能的元数据值**

可以在编码器 INF 文件中注册表的 "*设备参数\\功能*" 区域中指定元数据值。 应用程序可以使用这些元数据值来确定要实现或向用户公开的功能。

例如：

```INF
[Your driver's AddReg section]
HKR,Capabilities,,,
HKR,Capabilities,"{12345678-1234-1234-1234-12345678abcd}",,guid1
```

这会在编码器注册表设置的 "*设备参数\\功能*" 区域中创建元数据项 "{12345678-1234-1234-1234-12345678abcd} = guid1"。 如果注册表项尚不存在，则必须创建空行。

编码器筛选器可以在其 INF 文件中指定此类静态元数据以供应用程序使用。 例如，Windows XP Media Center Edition 检查编码器，它们指示它们是 Windows XP Media Center 版本兼容的。

### <a href="" id="the-filter-s-kernel-streaming-category"></a>**筛选器的内核流式处理类别**

内核流式处理筛选器必须指定它们所属的内核流式处理类别。 Microsoft 为常见类别定义了 Guid，包括编码器筛选器和多路复用器（mux）筛选器。

筛选器通过在其微型驱动程序的 INF 文件的筛选器部分的**AddInterface**指令中指定以下一个或多个 guid 来指示其各自的类别：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>内核流式处理类别 GUID</th>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>{19689BF6-C384-48FD-AD51-90E58C79F70B}</p></td>
<td><p>KSCATEGORY_ENCODER</p></td>
<td><p>为编码器筛选器指定此 GUID。</p></td>
</tr>
<tr class="even">
<td><p>{7A5DE1D3-01A1-452C-B481-4FA2B96271E8}</p></td>
<td><p>KSCATEGORY_MULTIPLEXER</p></td>
<td><p>为 mux 筛选器指定此 GUID。</p></td>
</tr>
</tbody>
</table>

 

若要注册编码器筛选器，请在驱动程序的*DDInstall*中指定 KSCATEGORY\_编码器 GUID。**接口**INF 文件部分。 例如：

```INF
[Your Driver's DDInstall.Interface section]
AddInterface=%KSCATEGORY_ENCODER%,%KSNAME_Filter%,MyEncoderDevice.AddInterface

[MyEncoderDevice.AddInterface]
AddReg=MyEncoderDevice.AddReg

[MyEncoderDevice.AddReg]
HKR,,CLSID,,%KSProxy.CLSID%
HKR,,FriendlyName,,%MyEncoderDeviceFriendlyName%

[Strings]
KSCATEGORY_ENCODER="{19689BF6-C384-48FD-AD51-90E58C79F70B}"
KSNAME_Filter="{9B365890-165F-11D0-A195-0020AFD156E4}"
KSProxy.CLSID="17CCA71B-ECD7-11D0-B908-00A0C9223196"
MyEncoderDeviceFriendlyName="My Encoder Device"
```

**注意：** 为*KSNAME\_筛选器*指定的 GUID 必须与在描述筛选器的[**KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构中指定的**ReferenceGuid**成员匹配。

 

 




