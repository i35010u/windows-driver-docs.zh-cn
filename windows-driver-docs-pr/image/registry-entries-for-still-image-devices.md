---
title: 静止图像设备的注册表项
description: 静止图像设备的注册表项
ms.assetid: cedc8afc-54c4-485e-989c-481fe30d899b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a7722bb95a39d2011d4ae1e5ec5c7893c7cbfb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525558"
---
# <a name="registry-entries-for-still-image-devices"></a>静止图像设备的注册表项





Microsoft STI 使用多个注册表条目，其中一些可以修改由供应商提供的组件。

### <a href="" id="ddk-vendor-modifiable-registry-values-si"></a>供应商可修改的注册表值

下表列出了预定义的注册表值名称和它们的含义。 在中定义常量*stireg.h*。 如果设备支持的静止图像，必须将值分配给"TwainDS"[推送模型](creating-push-model-aware-applications.md)。 为其他名称的值是可选的。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Constant</th>
<th>值名称字符串</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STI_DEVICE_VALUE_ICM_PROFILE</p></td>
<td><p>&quot;ICMProfile&quot;</p></td>
<td><p>REG_MULTI_SZ 类型包含两个设备的 ICM 配置文件的名称。</p></td>
</tr>
<tr class="even">
<td><p>STI_DEVICE_VALUE_ISIS_NAME</p></td>
<td><p>&quot;ISISDriverName&quot;</p></td>
<td><p>包含设备的 REG_SZ 类型&#39;s ISIS 驱动程序名称，例如&quot;epson.pxn&quot;。</p></td>
</tr>
<tr class="odd">
<td><p>STI_DEVICE_VALUE_TIMEOUT</p></td>
<td><p>&quot;PollTimeout&quot;</p></td>
<td><p>表示超时值，以毫秒为单位，轮询设备时应使用的 REG_DWORD 类型。 默认值为 1000 （1 秒）。</p></td>
</tr>
<tr class="even">
<td><p>STI_DEVICE_VALUE_TWAIN_NAME</p></td>
<td><p>&quot;TwainDS&quot;</p></td>
<td><p>REG_SZ 类型包含的设备的可显示的名称&#39;s TWAIN 数据源，如&quot;HP PictureScan 3.0&quot;。</p></td>
</tr>
</tbody>
</table>

 

客户端**StillImage**应调用 COM 接口[ **IStillImage::SetDeviceValue** ](https://msdn.microsoft.com/library/windows/hardware/ff543801)并[ **IStillImage::GetDeviceValue** ](https://msdn.microsoft.com/library/windows/hardware/ff543786)引用注册表。 映像微型驱动程序仍可以调用 Win32 注册表 API，指定接收的微型驱动程序的注册表项[ **IStiUSD::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff543824)方法。 此外可以在设置预定义的注册表条目的值[INF 文件](inf-files-for-still-image-devices.md)。

### <a name="customized-registry-values"></a>自定义的注册表值

静止图像的应用程序和微型驱动程序还可以在注册表中存储自定义的特定于设备的值。 例如，可以"用户设置"子项下存储用户选择从自定义的属性表页获取。

此外，在设置自定义的注册表项的值[INF 文件](inf-files-for-still-image-devices.md)通过包括**DeviceData**条目。

### <a href="" id="ddk-non-modifiable-registry-entries-si"></a>不可修改的注册表项

下表列出了供应商软件不应修改的注册表项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表项</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\StillImage\Logging\STICLI</strong></p></td>
<td><p>指定哪些供应商生成的消息写入到静止图像日志文件。 可以是以下位掩码的任意组合：</p>
<p>0x1-信息性消息</p>
<p>0x2-警告消息</p>
<p>0x4-错误消息</p>
<p>请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff543807" data-raw-source="[&lt;strong&gt;IStillImage::WriteToErrorLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543807)"> <strong>IStillImage::WriteToErrorLog</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\StillImage\Logging\STIMON</strong></p></td>
<td><p>指定哪些事件监视器消息写入到静止图像日志文件。 可以是以下位掩码的任意组合：</p>
<p>0x1-信息性消息</p>
<p>0x2-警告消息</p>
<p>0x4-错误消息</p></td>
</tr>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\Class{6BDD1FC6-810F-11D0-BEC7-08002BE2092F}</strong></p></td>
<td><p>包含有关已安装的静止图像设备信息。</p></td>
</tr>
<tr class="even">
<td><p><strong>HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\StillImage\Registered Applications</strong></p></td>
<td><p>包含已注册的图像处理应用程序的列表。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\DeviceClass{6bdd1fc6-810f-11d0-bec7-08002be2092f}</strong></p></td>
<td><p>包含有关已安装的静止图像设备接口的信息。</p></td>
</tr>
</tbody>
</table>

 

 

 




