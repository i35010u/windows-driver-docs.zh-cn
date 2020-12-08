---
title: IStiDevice COM 接口
description: IStiDevice COM 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dbf1a1186391a3b9b3c59da2a4d33bf78bd54d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816719"
---
# <a name="istidevice-com-interface"></a>IStiDevice COM 接口





**IStiDevice** COM 接口使应用程序能够与静态图像设备进行通信。 接口方法允许应用程序发送和接收数据和命令，运行诊断测试，接收 [静止图像设备事件](still-image-device-events.md)的通知，以及获取设备功能和状态信息。

可以通过调用 [ISTILLIMAGE COM 接口](istillimage-com-interface.md)的 **CreateDevice** 方法获取对 **IStiDevice** 接口的访问。 许多 **IStiDevice** 接口的方法通过调用 [IStiUSD COM 接口](istiusd-com-interface.md)定义的命名方法来实现。

下表列出并描述了 **IStiDevice** 接口提供的所有方法。 该表指示通常必须调用每个方法的客户端的类型。

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
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-devicereset" data-raw-source="[&lt;strong&gt;IStiDevice::DeviceReset&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-devicereset)"><strong>IStiDevice：:D eviceReset</strong></a></p></td>
<td><p>将静止图像设备重置为已知状态。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-diagnostic" data-raw-source="[&lt;strong&gt;IStiDevice::Diagnostic&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-diagnostic)"><strong>IStiDevice：:D 诊断</strong></a></p></td>
<td><p>对静止图像设备执行诊断测试。</p></td>
<td><p>扫描仪和照相机控制面板</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-escape" data-raw-source="[&lt;strong&gt;IStiDevice::Escape&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-escape)"><strong>IStiDevice：： Escape</strong></a></p></td>
<td><p>将特定于供应商的 i/o 操作请求发送到静止图像设备。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getcapabilities" data-raw-source="[&lt;strong&gt;IStiDevice::GetCapabilities&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getcapabilities)"><strong>IStiDevice：： GetCapabilities</strong></a></p></td>
<td><p>返回静止图像设备的功能。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlasterror" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastError&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlasterror)"><strong>IStiDevice：： GetLastError</strong></a></p></td>
<td><p>返回与静态图像设备关联的上一个已知错误。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlasterrorinfo" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastErrorInfo&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlasterrorinfo)"><strong>IStiDevice::GetLastErrorInfo</strong></a></p></td>
<td><p>返回有关与静态图像设备关联的上一个已知错误的信息。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastNotificationData&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata)"><strong>IStiDevice::GetLastNotificationData</strong></a></p></td>
<td><p>返回在静止图像设备上发生的最近事件的说明。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getstatus" data-raw-source="[&lt;strong&gt;IStiDevice::GetStatus&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getstatus)"><strong>IStiDevice：： GetStatus</strong></a></p></td>
<td><p>返回静止图像设备的状态信息。</p></td>
<td><p>图像获取 Api 和静态图像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-initialize" data-raw-source="[&lt;strong&gt;IStiDevice::Initialize&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-initialize)"><strong>IStiDevice：： Initialize</strong></a></p></td>
<td><p>初始化一个对象实例。</p></td>
<td><p>不直接调用</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-lockdevice" data-raw-source="[&lt;strong&gt;IStiDevice::LockDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-lockdevice)"><strong>IStiDevice::LockDevice</strong></a></p></td>
<td><p>锁定设备以供调用方独占使用。</p></td>
<td><p>所有 <strong>IStiDevice</strong> 接口客户端</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawreadcommand" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadCommand&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawreadcommand)"><strong>IStiDevice::RawReadCommand</strong></a></p></td>
<td><p>从静态图像设备读取命令信息。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawreaddata" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadData&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawreaddata)"><strong>IStiDevice::RawReadData</strong></a></p></td>
<td><p>从静止图像设备读取数据。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawwritecommand" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteCommand&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawwritecommand)"><strong>IStiDevice::RawWriteCommand</strong></a></p></td>
<td><p>将命令信息发送到静止图像设备。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawwritedata" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteData&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawwritedata)"><strong>IStiDevice::RawWriteData</strong></a></p></td>
<td><p>将数据写入静止图像设备。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-release" data-raw-source="[&lt;strong&gt;IStiDevice::Release&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-release)"><strong>IStiDevice：： Release</strong></a></p></td>
<td><p>关闭对象实例，并删除对 <strong>IStiDevice</strong> 接口的访问。</p></td>
<td><p>所有 <strong>IStiDevice</strong> 接口客户端</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-subscribe" data-raw-source="[&lt;strong&gt;IStiDevice::Subscribe&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-subscribe)"><strong>IStiDevice：：订阅</strong></a></p></td>
<td><p>注册调用方，接收设备事件的通知。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unlockdevice" data-raw-source="[&lt;strong&gt;IStiDevice::UnLockDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unlockdevice)"><strong>IStiDevice::UnLockDevice</strong></a></p></td>
<td><p>解锁设备。</p></td>
<td><p>所有 <strong>IStiDevice</strong> 接口客户端</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unsubscribe" data-raw-source="[&lt;strong&gt;IStiDevice::UnSubscribe&lt;/strong&gt;](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unsubscribe)"><strong>IStiDevice：：取消订阅</strong></a></p></td>
<td><p>从注册的应用程序列表中删除调用方，以接收设备事件的通知。</p></td>
<td><p>映像获取 Api</p></td>
</tr>
</tbody>
</table>

 

