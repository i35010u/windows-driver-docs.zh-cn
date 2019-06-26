---
title: 编码器安装和注册
description: 编码器安装和注册
ms.assetid: 6ce0c504-977a-4db5-b5ee-128b69ce8eba
keywords:
- 内核流式传输类别 WDK 编码器
- 编码器设备 WDK AVStream
- AVStream WDK，编码器设备
- 未压缩数据流 WDK AVStream
- 编码的流 WDK AVStream
- 音频编码器设备 WDK AVStream
- 视频编码器设备 WDK AVStream
- INF 文件 WDK 编码器
- 元数据 WDK 编码器
- KS 代理 WDK AVStream
- 内核流式处理代理 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d283b45c3df0f5490e55cf84220d7a62cb19cbc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384122"
---
# <a name="encoder-installation-and-registration"></a>编码器安装和注册


与编码器筛选器驱动程序的 INF 文件必须包含定义以下条目：

-   其他内核流式处理捕获组件

-   KsProxy 应公开的 COM 接口

-   元数据值，用于描述编码器筛选器的功能

-   流式处理类别筛选器的内核

### <a name="additional-kernel-streaming-capture-components"></a>**流式处理其他内核捕获组件**

使用为编码器设备必须引用安装驱动程序的 INF 文件*ks.inf*并*kscaptur.inf*中其\[DefaultInstall\]部分作为捕获驱动程序，因为这些文件将添加必要的编码器组件的支持。 例如：

```INF
[DefaultInstall]
include=ks.inf,kscaptur.inf
needs=[Your driver's DDInstall section],KS.Registration,KSCAPTUR.Registration.NT
```

### <a name="which-com-interface-ksproxy-should-expose"></a>**应公开的 COM 接口 KsProxy**

在中**AddReg**部分中的驱动程序的 INF 文件中，指定以下三个 Guid，以指示 COM 接口的插件 KsProxy (*encapi.dll*) 应公开给客户端。 COM 接口取决于你在编码器筛选器中实现的属性支持：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>接口的 GUID</th>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>{B43C4EEC-8C32-4791-9102-508ADA5EE8E7}</p></td>
<td><p><strong>CLSID_IVideoEncoderProxy</strong></p></td>
<td><p>指定要导致 KsProxy 公开此 GUID <strong>IVideoEncoder</strong> （适用于使用由 Microsoft 提供的编码器支持的较旧一代的向后兼容） 的 COM 接口。 客户端必须派生此接口的位置<strong>IEncoderAPI</strong> COM 接口。</p></td>
</tr>
<tr class="even">
<td><p>{7FF0997A-1999-4286-A73C-622B8814E7EB}</p></td>
<td><p><strong>CLSID_ICodecAPIProxy</strong></p></td>
<td><p>指定要导致 KsProxy 公开此 GUID <strong>ICodecAPI</strong> COM 接口 （用于非视频编码设备，例如仅限音频的编码器）。</p></td>
</tr>
<tr class="odd">
<td><p>{B05DABD9-56E5-4FDC-AFA4-8A47E91F1C9C}</p></td>
<td><p><strong>CLSID_IVideoEncoderCodecAPIProxy</strong></p></td>
<td><p>指定此 GUID 来导致 KsProxy 公开这两<strong>IVideoEncoder</strong>并<strong>ICodecAPI</strong> COM 接口 （适用于向后和向前兼容性）。</p></td>
</tr>
</tbody>
</table>

 

例如：

```INF
[Your driver's AddReg section]
HKR,Interfaces\{B43C4EEC-8C32-4791-9102-508ADA5EE8E7},,,
```

这将导致 KsProxy 仅公开**IVideoEncoder** (**CLSID\_IVideoEncoderProxy**) COM 接口。

这些 COM 接口都记录在 Windows Sdk for Windows XP SP1 和更高版本的 DirectX 9 的 DirectShow 部分中。

### <a href="" id="metadata-values-that-advertise-the-encoder-filter-s-capabilities"></a>**播发编码器筛选器的功能的元数据值**

可以指定元数据中的值*设备参数\\功能*注册表编码器的 INF 文件中的区域。 应用程序可以使用这些元数据值以确定哪些功能来实现或向用户公开。

例如：

```INF
[Your driver's AddReg section]
HKR,Capabilities,,,
HKR,Capabilities,"{12345678-1234-1234-1234-12345678abcd}",,guid1
```

这将创建元数据项"{12345678-1234-1234-1234-12345678abcd} = guid1"中*设备参数\\功能*编码器的注册表设置的区域。 空的行才可创建注册表项，如果尚不存在。

编码器过滤器可能由应用程序在使用其 INF 文件中指定此类静态元数据。 例如，Windows XP Media Center Edition 检查指示它们是 Windows XP Media Center Edition 兼容的编码器。

### <a href="" id="the-filter-s-kernel-streaming-category"></a>**流式处理类别筛选器的内核**

流式处理筛选器的内核必须指定流式处理到其所属的类别的内核。 Microsoft 为常见的类别，其中包括编码器筛选器和多路复用器 (mux) 筛选器定义 Guid。

筛选器通过指定一个或多个中的以下 Guid 指示它们各自的类别**AddInterface**其微型驱动程序的 INF 文件的筛选器的一部分的指令：

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
<td><p>指定此编码器筛选器的 GUID。</p></td>
</tr>
<tr class="even">
<td><p>{7A5DE1D3-01A1-452C-B481-4FA2B96271E8}</p></td>
<td><p>KSCATEGORY_MULTIPLEXER</p></td>
<td><p>指定此 GUID mux 筛选器。</p></td>
</tr>
</tbody>
</table>

 

若要注册一个编码器筛选器，指定 KSCATEGORY\_您的驱动程序中的编码器 GUID *DDInstall*。**接口**INF 文件部分。 例如：

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

**注意：** 为指定的 GUID *KSNAME\_筛选器*必须匹配**ReferenceGuid**中指定的成员[ **KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)结构，描述您的筛选器。

 

 




