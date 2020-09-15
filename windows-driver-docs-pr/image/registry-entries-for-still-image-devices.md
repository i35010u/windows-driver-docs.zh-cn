---
title: 静态图像设备的注册表项
description: 静态图像设备的注册表项
ms.assetid: cedc8afc-54c4-485e-989c-481fe30d899b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c80a003338d1bf6afa66612abc82d697ab616937
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105012"
---
# <a name="registry-entries-for-still-image-devices"></a>静态图像设备的注册表项





Microsoft STI 利用多个注册表项，其中一些注册表项可以由供应商提供的组件修改。

### <a name="vendor-modifiable-registry-values"></a><a href="" id="ddk-vendor-modifiable-registry-values-si"></a>供应商可修改的注册表值

下表列出了预定义的注册表值名称及其含义。 常量在 *stireg*中定义。 如果设备支持静止图像 [推送模式](creating-push-model-aware-applications.md)，则必须将该值分配给 "TwainDS"。 其他名称的值是可选的。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>常数</th>
<th>值名称字符串</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STI_DEVICE_VALUE_ICM_PROFILE</p></td>
<td><p>"ICMProfile"</p></td>
<td><p>REG_MULTI_SZ 类型，包含设备的 ICM 配置文件的名称。</p></td>
</tr>
<tr class="even">
<td><p>STI_DEVICE_VALUE_ISIS_NAME</p></td>
<td><p>"ISISDriverName"</p></td>
<td><p>REG_SZ 类型，包含设备的 ISIS 驱动程序名称，例如 "pxn"。</p></td>
</tr>
<tr class="odd">
<td><p>STI_DEVICE_VALUE_TIMEOUT</p></td>
<td><p>"PollTimeout"</p></td>
<td><p>REG_DWORD 类型，表示轮询设备时应使用的超时值（以毫秒为单位）。 默认值为 1000（1 秒）。</p></td>
</tr>
<tr class="even">
<td><p>STI_DEVICE_VALUE_TWAIN_NAME</p></td>
<td><p>"TwainDS"</p></td>
<td><p>REG_SZ 类型，包含设备的 TWAIN 数据源的可显示名称，如 "HP PictureScan 3.0"。</p></td>
</tr>
</tbody>
</table>

 

**StillImage** COM 接口的客户端应调用[**IStillImage：： SetDeviceValue**](/previous-versions/windows/hardware/drivers/ff543801(v=vs.85))和[**IStillImage：： GetDeviceValue**](/previous-versions/windows/hardware/drivers/ff543786(v=vs.85))以引用注册表。 静止图像微型驱动程序可以调用 Win32 注册表 API，并指定微型驱动程序的 [**IStiUSD：： Initialize**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize) 方法接收的注册表项。 还可以从 [INF 文件](inf-files-for-still-image-devices.md)中设置预定义注册表项的值。

### <a name="customized-registry-values"></a>自定义注册表值

静止的图像应用程序和微型驱动程序还可以在注册表中存储特定于设备的自定义值。 例如，从自定义属性表页面获取的用户选择可能存储在 "UserSettings" 子项下。

此外，还可以通过包含**DeviceData**项在[INF 文件](inf-files-for-still-image-devices.md)中设置自定义注册表项的值。

### <a name="nonmodifiable-registry-entries"></a><a href="" id="ddk-non-modifiable-registry-entries-si"></a>不可更改的注册表项

下表列出了不应由供应商软件修改的注册表项。

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
<td><p>指定哪些供应商生成的消息将写入到静态图像日志文件中。 可以是下列位掩码的任意组合：</p>
<p>0x1-信息性消息</p>
<p>0x2-警告消息</p>
<p>0x4-错误消息</p>
<p>请参阅 <a href="/previous-versions/windows/hardware/drivers/ff543807(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::WriteToErrorLog&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543807(v=vs.85))"><strong>IStillImage：： WriteToErrorLog</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\StillImage\Logging\STIMON</strong></p></td>
<td><p>指定将哪些事件监视器消息写入到静态图像日志文件中。 可以是下列位掩码的任意组合：</p>
<p>0x1-信息性消息</p>
<p>0x2-警告消息</p>
<p>0x4-错误消息</p></td>
</tr>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\Class{6BDD1FC6-810F-11D0-BEC7-08002BE2092F}</strong></p></td>
<td><p>包含有关已安装的静止图像设备的信息。</p></td>
</tr>
<tr class="even">
<td><p><strong>HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\StillImage\Registered 应用程序</strong></p></td>
<td><p>包含已注册的图像应用程序的列表。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\DeviceClass{6bdd1fc6-810f-11d0-bec7-08002be2092f}</strong></p></td>
<td><p>包含有关已安装的静止映像设备接口的信息。</p></td>
</tr>
</tbody>
</table>

 

