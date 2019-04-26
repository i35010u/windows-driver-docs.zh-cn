---
title: IStiDevice COM 接口
description: IStiDevice COM 接口
ms.assetid: b026fb74-9ce6-4d4e-8a5b-402731904064
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47ad78260900a330768d124e6e39850a31190098
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326998"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543733" data-raw-source="[&lt;strong&gt;IStiDevice::DeviceReset&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543733)"><strong>IStiDevice::DeviceReset</strong></a></p></td>
<td><p>将静态图像设备重置为已知状态。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543736" data-raw-source="[&lt;strong&gt;IStiDevice::Diagnostic&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543736)"><strong>IStiDevice::Diagnostic</strong></a></p></td>
<td><p>静态图像设备上执行诊断测试。</p></td>
<td><p>扫描仪和照相机控件面板</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543740" data-raw-source="[&lt;strong&gt;IStiDevice::Escape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543740)"><strong>IStiDevice::Escape</strong></a></p></td>
<td><p>将特定于供应商的 I/O 操作的请求发送到静态图像设备。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543745" data-raw-source="[&lt;strong&gt;IStiDevice::GetCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543745)"><strong>IStiDevice::GetCapabilities</strong></a></p></td>
<td><p>返回一个静态的图像设备的功能。</p></td>
<td><p>静止图像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543747" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543747)"><strong>IStiDevice::GetLastError</strong></a></p></td>
<td><p>返回与静态图像设备相关联的最后一个已知的错误。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543749" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastErrorInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543749)"><strong>IStiDevice::GetLastErrorInfo</strong></a></p></td>
<td><p>返回有关与静态图像设备相关联的最后一个已知错误的信息。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543751" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastNotificationData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543751)"><strong>IStiDevice::GetLastNotificationData</strong></a></p></td>
<td><p>返回的静态图像设备发生的最新事件的描述。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543752" data-raw-source="[&lt;strong&gt;IStiDevice::GetStatus&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543752)"><strong>IStiDevice::GetStatus</strong></a></p></td>
<td><p>返回静态图像设备状态信息。</p></td>
<td><p>图像获取 Api 和仍映像事件监视器</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543754" data-raw-source="[&lt;strong&gt;IStiDevice::Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543754)"><strong>IStiDevice::Initialize</strong></a></p></td>
<td><p>初始化对象实例。</p></td>
<td><p>不直接调用</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543756" data-raw-source="[&lt;strong&gt;IStiDevice::LockDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543756)"><strong>IStiDevice::LockDevice</strong></a></p></td>
<td><p>锁定供独占使用由调用方的设备。</p></td>
<td><p>所有<strong>IStiDevice</strong>接口客户端</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543758" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543758)"><strong>IStiDevice::RawReadCommand</strong></a></p></td>
<td><p>读取命令从静态图像设备信息。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543760" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543760)"><strong>IStiDevice::RawReadData</strong></a></p></td>
<td><p>从静态图像设备读取数据。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543762" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543762)"><strong>IStiDevice::RawWriteCommand</strong></a></p></td>
<td><p>发送命令到静态图像设备信息。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543764" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543764)"><strong>IStiDevice::RawWriteData</strong></a></p></td>
<td><p>将数据写入到静态图像设备。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543765" data-raw-source="[&lt;strong&gt;IStiDevice::Release&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543765)"><strong>IStiDevice::Release</strong></a></p></td>
<td><p>关闭对象实例，并删除对访问权限<strong>IStiDevice</strong>接口。</p></td>
<td><p>所有<strong>IStiDevice</strong>接口客户端</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543768" data-raw-source="[&lt;strong&gt;IStiDevice::Subscribe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543768)"><strong>IStiDevice::Subscribe</strong></a></p></td>
<td><p>注册使调用方接收设备事件的通知。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543770" data-raw-source="[&lt;strong&gt;IStiDevice::UnLockDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543770)"><strong>IStiDevice::UnLockDevice</strong></a></p></td>
<td><p>解锁设备。</p></td>
<td><p>所有<strong>IStiDevice</strong>接口客户端</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543773" data-raw-source="[&lt;strong&gt;IStiDevice::UnSubscribe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543773)"><strong>IStiDevice::UnSubscribe</strong></a></p></td>
<td><p>注册以接收通知的设备事件的应用程序列表中移除调用方。</p></td>
<td><p>图像采集 Api</p></td>
</tr>
</tbody>
</table>

 

 

 




