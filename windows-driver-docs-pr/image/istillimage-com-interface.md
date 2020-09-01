---
title: IStillImage COM 接口
description: IStillImage COM 接口
ms.assetid: eb60a3fd-e7e2-4d3c-973e-af8cb3c3c511
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b59d5d333b79e64a535a857284d35ef13db01017
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186477"
---
# <a name="istillimage-com-interface"></a>IStillImage COM 接口





**IStillImage** COM 接口提供对[静止图像事件监视器](overview-of-sti-components.md#ddk-still-image-event-monitor-si)的访问，因此应用程序可将其自身注册为 "推送模型感知"。 应用程序可以使用此接口来获取有关系统的静止图像设备的信息。

接口提供一些应用程序管理功能，例如启用事件通知和启动应用程序，以供自定义的应用程序控制软件使用。

此外， **IStillImage** 接口提供对 [IStiDevice COM 接口](istidevice-com-interface.md)的访问权限，使应用程序能够对静止图像设备执行 i/o 操作。

下表列出并描述了 **IStillImage** 接口的所有方法。 该表指示通常必须调用每个方法的客户端的类型。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
<th>典型调用方</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::CreateDevice&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))"><strong>IStillImage::CreateDevice</strong></a></p></td>
<td><p>创建 COM 对象的实例，该对象定义 <strong>IStiDevice</strong> 接口，并返回一个指向接口的指针。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543780(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::EnableHwNotifications&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543780(v=vs.85))"><strong>IStillImage::EnableHwNotifications</strong></a></p></td>
<td><p>当指定设备的 <a href="still-image-device-events.md" data-raw-source="[Still Image Device Events](still-image-device-events.md)">静止图像设备事件</a> 发生时，启用或禁用应用程序通知。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543782(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceInfo&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543782(v=vs.85))"><strong>IStillImage::GetDeviceInfo</strong></a></p></td>
<td><p>返回指定的静止图像设备的硬件特征。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543784(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceList&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543784(v=vs.85))"><strong>IStillImage::GetDeviceList</strong></a></p></td>
<td><p>返回所有已安装的静止图像设备的硬件特征。</p></td>
<td><p>扫描仪和照相机控制面板，图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543786(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceValue&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543786(v=vs.85))"><strong>IStillImage::GetDeviceValue</strong></a></p></td>
<td><p>返回与指定的静止图像设备关联的注册表信息。</p></td>
<td><p>图像获取 Api、扫描仪和照相机控制面板</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543788(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::GetHwNotificationState&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543788(v=vs.85))"><strong>IStillImage::GetHwNotificationState</strong></a></p></td>
<td><p>指示当指定设备上出现静止图像设备事件时是否通知应用程序。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543790(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::GetSTILaunchInformation&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543790(v=vs.85))"><strong>IStillImage::GetSTILaunchInformation</strong></a></p></td>
<td><p>返回调用静止映像应用程序启动的原因（如果 "静止映像" 事件监视器已启动）。</p></td>
<td><p>推送模型感知应用程序</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543793(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::Initialize&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543793(v=vs.85))"><strong>IStillImage：： Initialize</strong></a></p></td>
<td><p>初始化对象实例。</p></td>
<td><p>不直接调用</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543796(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::LaunchApplicationForDevice&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543796(v=vs.85))"><strong>IStillImage::LaunchApplicationForDevice</strong></a></p></td>
<td><p>为指定的静止图像设备启动指定的应用程序。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543798(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::RegisterLaunchApplication&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543798(v=vs.85))"><strong>IStillImage::RegisterLaunchApplication</strong></a></p></td>
<td><p>将应用程序添加到推送模型识别应用程序的 "静止映像" 事件监视器列表。</p></td>
<td><p>推送模型识别应用程序或其安装程序</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543799(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::Release&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543799(v=vs.85))"><strong>IStillImage：： Release</strong></a></p></td>
<td><p>关闭对象实例，并删除对 <strong>IStillImage</strong> 接口的访问。</p></td>
<td><p>所有 <strong>IStillImage</strong> 接口客户端</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543801(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::SetDeviceValue&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543801(v=vs.85))"><strong>IStillImage::SetDeviceValue</strong></a></p></td>
<td><p>为指定的静止图像设备设置注册表信息。</p></td>
<td><p>扫描仪和照相机控制面板</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543803(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::SetupDeviceParameters&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543803(v=vs.85))"><strong>IStillImage::SetupDeviceParameters</strong></a></p></td>
<td><p>允许 <strong>IStillImage</strong> 接口的客户端修改静止图像设备的存储特征。</p></td>
<td><p>扫描仪和照相机控制面板</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543804(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::StiCreateInstance&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543804(v=vs.85))"><strong>IStillImage::StiCreateInstance</strong></a></p></td>
<td><p>创建 COM 对象的实例，该对象定义 <strong>IStillImage</strong> 接口，并返回一个指向接口的指针。</p></td>
<td><p>所有 <strong>IStillImage</strong> 接口客户端</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543806(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::UnregisterLaunchApplication&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543806(v=vs.85))"><strong>IStillImage::UnregisterLaunchApplication</strong></a></p></td>
<td><p>从静止模型识别应用程序的 "静态映像" 事件监视器列表中删除应用程序。</p></td>
<td><p>推送模型识别应用程序或其安装程序</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543807(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::WriteToErrorLog&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff543807(v=vs.85))"><strong>IStillImage::WriteToErrorLog</strong></a></p></td>
<td><p>将消息写入静止图像错误日志。</p></td>
<td><p>所有 <strong>IStillImage</strong> 接口客户端</p></td>
</tr>
</tbody>
</table>

 

 

