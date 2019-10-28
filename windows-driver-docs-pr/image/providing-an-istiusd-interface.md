---
title: 提供了 IStiUSD 界面
description: 提供了 IStiUSD 界面
ms.assetid: ed15b56b-0b63-4983-a4ff-df379a2b9de9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dab282f73d6bce43b50096639bb926789ba9f2e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840767"
---
# <a name="providing-an-istiusd-interface"></a>提供了 IStiUSD 界面





WIA 在 STI 上生成。 为了确保 WIA 微型驱动程序与 STI 的集成，微型驱动程序必须实现从[IStiUSD 接口方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)派生的接口。 此接口必须存在于 WIA 微型驱动程序中。 **IStiUSD**接口用于管理设备（如加载驱动程序），这是[IStiDevice 接口方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)与静态图像设备通信的方式。 微型驱动程序必须完全实现从[**IStiUSD：： Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)方法派生的接口，才能由 WIA 服务加载。

通常， **IStiUSD**接口方法由**IStiDevice**接口定义的类似命名方法调用。 微型驱动程序通常通过调用相应的内核模式驱动程序来实现**IStiUSD**接口方法。 每个微型驱动程序都必须定义所有接口方法，但如果没有所需的方法，只需返回不受支持的 STIERR\_。

有关微型驱动程序如何实现**IStiUSD**接口的示例，请参阅*wiacam*照相机示例微型驱动程序文件*IStiUSD。*

下表列出并描述了**IStiUSD**接口定义的所有方法。 标识必须实现或由 WIA 微型驱动程序有条件地实现的方法。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-devicereset" data-raw-source="[&lt;strong&gt;IStiUSD::DeviceReset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-devicereset)"><strong>IStiUSD：:D eviceReset</strong></a></p></td>
<td><p>将静止图像设备重置为已知的初始化状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic" data-raw-source="[&lt;strong&gt;IStiUSD::Diagnostic&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic)"><strong>IStiUSD：:D 诊断</strong></a></p></td>
<td><p>在静止图像设备上运行诊断测试。 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape" data-raw-source="[&lt;strong&gt;IStiUSD::Escape&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)"><strong>IStiUSD：： Escape</strong></a></p></td>
<td><p>对静止图像设备执行特定于供应商的 i/o 操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities" data-raw-source="[&lt;strong&gt;IStiUSD::GetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)"><strong>IStiUSD：： GetCapabilities</strong></a></p></td>
<td><p>返回静止图像设备的功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo" data-raw-source="[&lt;strong&gt;IStiUSD::GetLastErrorInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo)"><strong>IStiUSD::GetLastErrorInfo</strong></a></p></td>
<td><p>返回有关与静态图像设备关联的上一个已知错误的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata" data-raw-source="[&lt;strong&gt;IStiUSD::GetNotificationData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)"><strong>IStiUSD::GetNotificationData</strong></a></p></td>
<td><p>返回在静止图像设备上发生的最近事件的说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus" data-raw-source="[&lt;strong&gt;IStiUSD::GetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)"><strong>IStiUSD：： GetStatus</strong></a></p></td>
<td><p>返回静止图像设备的状态。 如果 WIA 微型驱动程序的设备具有可生成事件的对象（如按钮），则必须实现此方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize" data-raw-source="[&lt;strong&gt;IStiUSD::Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)"><strong>IStiUSD：： Initialize</strong></a></p></td>
<td><p>初始化定义<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[IStiUSD interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">IStiUSD 接口</a>的 COM 对象的实例。 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice" data-raw-source="[&lt;strong&gt;IStiUSD::LockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)"><strong>IStiUSD::LockDevice</strong></a></p></td>
<td><p>锁定设备以供调用方独占使用。 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreadcommand" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreadcommand)"><strong>IStiUSD::RawReadCommand</strong></a></p></td>
<td><p>从静态图像设备读取命令信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata)"><strong>IStiUSD::RawReadData</strong></a></p></td>
<td><p>从静止图像设备读取数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand)"><strong>IStiUSD::RawWriteCommand</strong></a></p></td>
<td><p>向静止图像设备写入命令信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata)"><strong>IStiUSD::RawWriteData</strong></a></p></td>
<td><p>将数据写入静止图像设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle" data-raw-source="[&lt;strong&gt;IStiUSD::SetNotificationHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)"><strong>IStiUSD::SetNotificationHandle</strong></a></p></td>
<td><p>指定微型驱动程序应用于向调用方通知设备事件的事件句柄。 如果 WIA 微型驱动程序的设备具有可生成事件的对象（如按钮），则必须实现此方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice" data-raw-source="[&lt;strong&gt;IStiUSD::UnLockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)"><strong>IStiUSD::UnLockDevice</strong></a></p></td>
<td><p>关闭设备端口。 WIA 微型驱动程序必须实现此方法。</p></td>
</tr>
</tbody>
</table>

 

 

 




