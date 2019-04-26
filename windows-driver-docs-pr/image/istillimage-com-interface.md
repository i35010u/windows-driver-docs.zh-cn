---
title: IStillImage COM 接口
description: IStillImage COM 接口
ms.assetid: eb60a3fd-e7e2-4d3c-973e-af8cb3c3c511
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab0bc581ed9f55041b2d45f82df87fcf6e40caf5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327033"
---
# <a name="istillimage-com-interface"></a>IStillImage COM 接口





**IStillImage** COM 接口提供对访问[静止图像事件监控程序](overview-of-sti-components.md#ddk-still-image-event-monitor-si)使应用程序可以将自身注册为"推送模型注意"。 应用程序可以使用此接口来获取有关系统的静止图像设备信息。

该接口提供某些应用程序管理功能，例如启用事件通知和启动应用程序，以供自定义应用程序管理软件。

此外， **IStillImage**接口提供对访问[IStiDevice COM 接口](istidevice-com-interface.md)，它允许应用程序执行静止图像设备上的 I/O 操作。

下表列出并描述的所有**IStillImage**接口的方法。 此表指示通常必须调用每个方法的客户端的类型。

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
<th>典型的调用方</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543778" data-raw-source="[&lt;strong&gt;IStillImage::CreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543778)"><strong>IStillImage::CreateDevice</strong></a></p></td>
<td><p>创建定义的 COM 对象的实例<strong>IStiDevice</strong>接口，并返回指向该接口的指针。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543780" data-raw-source="[&lt;strong&gt;IStillImage::EnableHwNotifications&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543780)"><strong>IStillImage::EnableHwNotifications</strong></a></p></td>
<td><p>启用或禁用通知的应用程序时<a href="still-image-device-events.md" data-raw-source="[Still Image Device Events](still-image-device-events.md)">仍映像设备事件</a>发生指定的设备。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543782" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543782)"><strong>IStillImage::GetDeviceInfo</strong></a></p></td>
<td><p>返回指定静止图像设备的硬件特征。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543784" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543784)"><strong>IStillImage::GetDeviceList</strong></a></p></td>
<td><p>返回所有的硬件特征仍安装映像的设备。</p></td>
<td><p>扫描仪和照相机控件面板中，图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543786" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543786)"><strong>IStillImage::GetDeviceValue</strong></a></p></td>
<td><p>返回与指定的静止图像设备相关联的注册表信息。</p></td>
<td><p>图像采集 Api、 扫描仪和照相机控件面板</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543788" data-raw-source="[&lt;strong&gt;IStillImage::GetHwNotificationState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543788)"><strong>IStillImage::GetHwNotificationState</strong></a></p></td>
<td><p>指示映像设备事件仍在指定的设备上发生时是否会通知应用程序。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543790" data-raw-source="[&lt;strong&gt;IStillImage::GetSTILaunchInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543790)"><strong>IStillImage::GetSTILaunchInformation</strong></a></p></td>
<td><p>返回已启动调用静止图像的应用程序的原因，如果静止图像事件监视器启动它。</p></td>
<td><p>推送模型识别应用程序</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543793" data-raw-source="[&lt;strong&gt;IStillImage::Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543793)"><strong>IStillImage::Initialize</strong></a></p></td>
<td><p>初始化的对象实例。</p></td>
<td><p>不直接调用</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543796" data-raw-source="[&lt;strong&gt;IStillImage::LaunchApplicationForDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543796)"><strong>IStillImage::LaunchApplicationForDevice</strong></a></p></td>
<td><p>启动指定的静止图像设备指定的应用程序。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543798" data-raw-source="[&lt;strong&gt;IStillImage::RegisterLaunchApplication&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543798)"><strong>IStillImage::RegisterLaunchApplication</strong></a></p></td>
<td><p>将添加到静止图像事件监视器的列表的推送模型识别应用程序的应用程序。</p></td>
<td><p>推送模型识别应用程序或它们的安装程序</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543799" data-raw-source="[&lt;strong&gt;IStillImage::Release&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543799)"><strong>IStillImage::Release</strong></a></p></td>
<td><p>关闭对象实例，并删除对访问权限<strong>IStillImage</strong>接口。</p></td>
<td><p>所有<strong>IStillImage</strong>接口客户端</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543801" data-raw-source="[&lt;strong&gt;IStillImage::SetDeviceValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543801)"><strong>IStillImage::SetDeviceValue</strong></a></p></td>
<td><p>设置指定静止图像设备的注册表信息。</p></td>
<td><p>扫描仪和照相机控件面板</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543803" data-raw-source="[&lt;strong&gt;IStillImage::SetupDeviceParameters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543803)"><strong>IStillImage::SetupDeviceParameters</strong></a></p></td>
<td><p>允许的客户端<strong>IStillImage</strong>界面，用于修改静态图像设备存储特征。</p></td>
<td><p>扫描仪和照相机控件面板</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543804" data-raw-source="[&lt;strong&gt;IStillImage::StiCreateInstance&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543804)"><strong>IStillImage::StiCreateInstance</strong></a></p></td>
<td><p>创建定义的 COM 对象的实例<strong>IStillImage</strong>接口，并返回指向该接口的指针。</p></td>
<td><p>所有<strong>IStillImage</strong>接口客户端</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543806" data-raw-source="[&lt;strong&gt;IStillImage::UnregisterLaunchApplication&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543806)"><strong>IStillImage::UnregisterLaunchApplication</strong></a></p></td>
<td><p>推送模型识别应用程序静止图像事件监视器的列表中移除应用程序。</p></td>
<td><p>推送模型识别应用程序或它们的安装程序</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543807" data-raw-source="[&lt;strong&gt;IStillImage::WriteToErrorLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543807)"><strong>IStillImage::WriteToErrorLog</strong></a></p></td>
<td><p>静止图像错误日志中写入一条消息。</p></td>
<td><p>所有<strong>IStillImage</strong>接口客户端</p></td>
</tr>
</tbody>
</table>

 

 

 




