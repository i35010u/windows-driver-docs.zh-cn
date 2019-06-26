---
title: IStiDevice COM 接口
description: IStiDevice COM 接口
ms.assetid: b026fb74-9ce6-4d4e-8a5b-402731904064
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eca2a64e4a28dd377c95de15d5ecab2a9f5a707
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378916"
---
# <a name="istidevice-com-interface"></a>IStiDevice COM 接口





**IStiDevice** COM 接口提供了具有与通信的能力的应用程序静止图像的设备。 接口方法允许应用程序发送和接收数据和命令来运行诊断测试，以接收通知[仍映像设备事件](still-image-device-events.md)，并获取设备功能和状态信息。

访问权限**IStiDevice**接口获取通过调用**CreateDevice**方法[IStillImage COM 接口](istillimage-com-interface.md)。 许多**IStiDevice**接口的方法通过调用定义的名称类似的方法实现[IStiUSD COM 接口](istiusd-com-interface.md)。

下表列出并描述所有提供的方法**IStiDevice**接口。 此表指示通常必须调用每个方法的客户端的类型。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-devicereset" data-raw-source="[&lt;strong&gt;IStiDevice::DeviceReset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-devicereset)"><strong>IStiDevice::DeviceReset</strong></a></p></td>
<td><p>将静态图像设备重置为已知状态。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-diagnostic" data-raw-source="[&lt;strong&gt;IStiDevice::Diagnostic&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-diagnostic)"><strong>IStiDevice::Diagnostic</strong></a></p></td>
<td><p>静态图像设备上执行诊断测试。</p></td>
<td><p>扫描仪和照相机控件面板</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-escape" data-raw-source="[&lt;strong&gt;IStiDevice::Escape&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-escape)"><strong>IStiDevice::Escape</strong></a></p></td>
<td><p>将特定于供应商的 I/O 操作的请求发送到静态图像设备。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getcapabilities" data-raw-source="[&lt;strong&gt;IStiDevice::GetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getcapabilities)"><strong>IStiDevice::GetCapabilities</strong></a></p></td>
<td><p>返回一个静态的图像设备的功能。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlasterror" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlasterror)"><strong>IStiDevice::GetLastError</strong></a></p></td>
<td><p>返回与静态图像设备相关联的最后一个已知的错误。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlasterrorinfo" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastErrorInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlasterrorinfo)"><strong>IStiDevice::GetLastErrorInfo</strong></a></p></td>
<td><p>返回有关与静态图像设备相关联的最后一个已知错误的信息。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastNotificationData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata)"><strong>IStiDevice::GetLastNotificationData</strong></a></p></td>
<td><p>返回的静态图像设备发生的最新事件的描述。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getstatus" data-raw-source="[&lt;strong&gt;IStiDevice::GetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getstatus)"><strong>IStiDevice::GetStatus</strong></a></p></td>
<td><p>返回静态图像设备状态信息。</p></td>
<td><p>图像获取 Api 和仍映像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-initialize" data-raw-source="[&lt;strong&gt;IStiDevice::Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-initialize)"><strong>IStiDevice::Initialize</strong></a></p></td>
<td><p>初始化对象实例。</p></td>
<td><p>不直接调用</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-lockdevice" data-raw-source="[&lt;strong&gt;IStiDevice::LockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-lockdevice)"><strong>IStiDevice::LockDevice</strong></a></p></td>
<td><p>锁定供独占使用由调用方的设备。</p></td>
<td><p>所有<strong>IStiDevice</strong>接口客户端</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawreadcommand" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawreadcommand)"><strong>IStiDevice::RawReadCommand</strong></a></p></td>
<td><p>读取命令从静态图像设备信息。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawreaddata" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawreaddata)"><strong>IStiDevice::RawReadData</strong></a></p></td>
<td><p>从静态图像设备读取数据。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawwritecommand" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawwritecommand)"><strong>IStiDevice::RawWriteCommand</strong></a></p></td>
<td><p>发送命令到静态图像设备信息。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawwritedata" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawwritedata)"><strong>IStiDevice::RawWriteData</strong></a></p></td>
<td><p>将数据写入到静态图像设备。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-release" data-raw-source="[&lt;strong&gt;IStiDevice::Release&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-release)"><strong>IStiDevice::Release</strong></a></p></td>
<td><p>关闭对象实例，并删除对访问权限<strong>IStiDevice</strong>接口。</p></td>
<td><p>所有<strong>IStiDevice</strong>接口客户端</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-subscribe" data-raw-source="[&lt;strong&gt;IStiDevice::Subscribe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-subscribe)"><strong>IStiDevice::Subscribe</strong></a></p></td>
<td><p>注册使调用方接收设备事件的通知。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unlockdevice" data-raw-source="[&lt;strong&gt;IStiDevice::UnLockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unlockdevice)"><strong>IStiDevice::UnLockDevice</strong></a></p></td>
<td><p>解锁设备。</p></td>
<td><p>所有<strong>IStiDevice</strong>接口客户端</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unsubscribe" data-raw-source="[&lt;strong&gt;IStiDevice::UnSubscribe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unsubscribe)"><strong>IStiDevice::UnSubscribe</strong></a></p></td>
<td><p>注册以接收通知的设备事件的应用程序列表中移除调用方。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
</tbody>
</table>

 

 

 




