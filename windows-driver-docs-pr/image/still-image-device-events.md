---
title: 静态图像设备事件
description: 静态图像设备事件
ms.assetid: 5f9be89c-8442-4894-b2f6-a4d3558464bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e738fde61797cff31c11a9b554aa5f6edcef159
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386914"
---
# <a name="still-image-device-events"></a>静态图像设备事件





一个*仍映像设备事件*是高级别的软件应将通知，设备级别匹配项，如果该软件已请求此类通知。 用户模式下微型驱动程序负责定义大多数设备事件和事件发生时提供通知。 一般情况下，事件指示较高级别软件要执行某些操作需要。

典型的静止图像设备事件是按下按钮按下的检测。 例如，扫描程序可能会提供具有单独的按钮的用户，以启动扫描文本和照片。 按下按钮时，若要显示或存储映像需要较高级别软件。 静止图像事件监视器检测到事件已发生 (使用[IStiDevice COM 接口](istidevice-com-interface.md))，并且可以调用以前注册的静止图像应用程序 (使用[IStillImage COM 接口](istillimage-com-interface.md)).

仍由 Guid 表示映像设备事件。 在中*sti.h*，Microsoft 定义了以下静止图像设备事件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件的 GUID</th>
<th>用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>GUID_DeviceArrivedLaunch</strong></p></td>
<td><p>静态图像设备只是已附加到系统。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_ScanImage</strong></p></td>
<td><p>图像应扫描到的计算机。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_ScanFaxImage</strong></p></td>
<td><p>图像应扫描到计算机，然后传真。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_ScanPrintImage</strong></p></td>
<td><p>应扫描到计算机并打印图像。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_STIUserDefined1</strong></p></td>
<td><p>已按下的用户可定义按钮。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_STIUserDefined2</strong></p></td>
<td><p>已按下的用户可定义按钮。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_STIUserDefined3</strong></p></td>
<td><p>已按下的用户可定义按钮。</p></td>
</tr>
</tbody>
</table>

 

用户模式下微型驱动程序的开发人员应使用这些预定义的事件 Guid，只要有可能。 如果这些 Guid 不合适，则必须定义特定于设备的事件的 Guid。

若要定义静止图像设备事件，您必须：

-   指定每个事件的 GUID。

-   用户模式驱动程序的 INF 文件中包含每个 GUID。

在驱动程序的 INF 文件中，每个 GUID 规范必须包含一个星号 （即"所有应用程序"） 或特定应用程序，指示在事件发生时应启动的应用程序的列表。 静止图像事件监视器使用此列表提供为事件的应用程序的默认分配。 用户可以修改这些分配使用扫描仪和照相机控件面板。

### <a name="event-notification"></a>事件通知

该驱动程序必须监视设备 （使用任一异步 I/O 或轮询） 以确定与每个 GUID 关联的事件发生时。 根据设备功能，该驱动程序可以通知设备事件的匹配项的客户端以异步方式或通过响应请求来轮询设备。 能够提供通知的设备事件 （按这两种方法） 的所有驱动程序必须设置 STI\_GENCAP\_中设备的通知标志[ **STI\_DEV\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/ns-sti-_sti_dev_caps)结构。 支持轮询和非异步通知的驱动程序还必须设置 STI\_GENCAP\_轮询\_需要同一结构中的标志。 (还必须使用指示这些功能**功能**中的关键字[INF 文件静止图像设备](inf-files-for-still-image-devices.md)。)

如果驱动程序支持的事件的异步通知，事件监视调用[ **IStiUSD::SetNotificationHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-setnotificationhandle)请求通知，以及提供一个事件句柄。 设备事件发生时，该驱动程序必须通过调用通知事件监视器**SetEvent** （请参阅 Microsoft Windows SDK 文档），作为参数使用的事件句柄。 然后，客户端可以调用[ **IStiUSD::GetNotificationData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getnotificationdata)若要获取该事件的 GUID。

如果轮询是必需的该事件监视调用[ **IStiUSD::GetStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getstatus)若要轮询的驱动程序，又必须轮询中的设备并返回结果[ **STI\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/ns-sti-_sti_device_status)结构。

 

 




