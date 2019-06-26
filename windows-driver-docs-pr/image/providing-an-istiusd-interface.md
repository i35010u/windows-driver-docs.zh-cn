---
title: 提供了 IStiUSD 界面
description: 提供了 IStiUSD 界面
ms.assetid: ed15b56b-0b63-4983-a4ff-df379a2b9de9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d11e17a702c58a2025e997326e6d1fe35e99bf4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376503"
---
# <a name="providing-an-istiusd-interface"></a>提供了 IStiUSD 界面





WIA STI 上生成。 为了确保与 STI WIA 微型驱动程序的集成，微型驱动程序必须实现的接口派生自[IStiUSD 接口方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)。 此接口必须存在 WIA 微型驱动程序中。 **IStiUSD**接口用于管理设备 （如加载驱动程序），并且是方式的情况[IStiDevice 接口方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)与静止图像设备进行通信。 微型驱动程序必须完全实现的接口派生自[ **IStiUSD::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)方法，以通过 WIA 服务加载。

通常情况下， **IStiUSD**定义的类似的命名方法会调用接口方法**IStiDevice**接口。 微型驱动程序通常实现**IStiUSD**接口方法通过调用适当的内核模式驱动程序。 每个微型驱动程序必须定义接口中的所有方法，但如果不是一种方法需要则可以只返回 STIERR\_不受支持。

请参阅*wiacam*照相机示例微型驱动程序文件*IStiUSD.cpp*，以举例说明如何实现微型驱动程序**IStiUSD**接口。

下表列出并描述所有定义的方法**IStiUSD**接口。 方法必须实现或有条件地实现 WIA 微型驱动程序的标识。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-devicereset" data-raw-source="[&lt;strong&gt;IStiUSD::DeviceReset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-devicereset)"><strong>IStiUSD::DeviceReset</strong></a></p></td>
<td><p>将静态图像设备重置为已知的初始化状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-diagnostic" data-raw-source="[&lt;strong&gt;IStiUSD::Diagnostic&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-diagnostic)"><strong>IStiUSD::Diagnostic</strong></a></p></td>
<td><p>在静态图像设备上运行诊断测试。 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-escape" data-raw-source="[&lt;strong&gt;IStiUSD::Escape&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-escape)"><strong>IStiUSD::Escape</strong></a></p></td>
<td><p>执行静态图像设备上的特定于供应商的 I/O 操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getcapabilities" data-raw-source="[&lt;strong&gt;IStiUSD::GetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getcapabilities)"><strong>IStiUSD::GetCapabilities</strong></a></p></td>
<td><p>返回一个静态的图像设备的功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getlasterrorinfo" data-raw-source="[&lt;strong&gt;IStiUSD::GetLastErrorInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getlasterrorinfo)"><strong>IStiUSD::GetLastErrorInfo</strong></a></p></td>
<td><p>返回有关与静态图像设备相关联的最后一个已知错误的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getnotificationdata" data-raw-source="[&lt;strong&gt;IStiUSD::GetNotificationData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getnotificationdata)"><strong>IStiUSD::GetNotificationData</strong></a></p></td>
<td><p>返回的静态图像设备发生的最新事件的描述。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getstatus" data-raw-source="[&lt;strong&gt;IStiUSD::GetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getstatus)"><strong>IStiUSD::GetStatus</strong></a></p></td>
<td><p>返回静态图像设备的状态。 如果其设备对象，例如按钮，可以生成事件的 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize" data-raw-source="[&lt;strong&gt;IStiUSD::Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)"><strong>IStiUSD::Initialize</strong></a></p></td>
<td><p>初始化一个实例定义的 COM 对象<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[IStiUSD interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">IStiUSD 接口</a>。 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-lockdevice" data-raw-source="[&lt;strong&gt;IStiUSD::LockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-lockdevice)"><strong>IStiUSD::LockDevice</strong></a></p></td>
<td><p>锁定供独占使用由调用方的设备。 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreadcommand" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreadcommand)"><strong>IStiUSD::RawReadCommand</strong></a></p></td>
<td><p>读取命令从静态图像设备信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreaddata" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreaddata)"><strong>IStiUSD::RawReadData</strong></a></p></td>
<td><p>从静态图像设备读取数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritecommand" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritecommand)"><strong>IStiUSD::RawWriteCommand</strong></a></p></td>
<td><p>写入静态图像设备命令的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritedata" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritedata)"><strong>IStiUSD::RawWriteData</strong></a></p></td>
<td><p>将数据写入到静态图像设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-setnotificationhandle" data-raw-source="[&lt;strong&gt;IStiUSD::SetNotificationHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-setnotificationhandle)"><strong>IStiUSD::SetNotificationHandle</strong></a></p></td>
<td><p>指定应使用微型驱动程序通知设备事件的调用方的事件句柄。 如果其设备对象，例如按钮，可以生成事件的 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-unlockdevice" data-raw-source="[&lt;strong&gt;IStiUSD::UnLockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-unlockdevice)"><strong>IStiUSD::UnLockDevice</strong></a></p></td>
<td><p>关闭设备端口。 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
</tbody>
</table>

 

 

 




