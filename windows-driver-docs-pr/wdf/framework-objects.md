---
title: 框架对象
description: 框架对象
ms.assetid: bd9ec812-205d-4f9a-b85b-4e3a2f7556bd
keywords:
- 列出 UMDF 对象 WDK，
- 列出的 framework 对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a80824e0662eb8d652acd84c97cdee8108a29bd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384452"
---
# <a name="framework-objects"></a>框架对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下表提供了有关每个框架对象、 对象的接口的核心框架对象有关的详细信息的链接的基本信息。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">对象名称</th>
<th align="left">ObjectInterface</th>
<th align="left">用途</th>
<th align="left">Defaultparent</th>
<th align="left">可以驱动程序 overridedefaultparent？</th>
<th align="left">可以自己的驱动程序？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="framework-driver-object.md" data-raw-source="[Driver object](framework-driver-object.md)">驱动程序对象</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver" data-raw-source="[IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)">IWDFDriver</a></p></td>
<td align="left"><p>表示一个驱动程序</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-device-object.md" data-raw-source="[Device object](framework-device-object.md)">设备对象</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice" data-raw-source="[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)">IWDFDevice</a></p></td>
<td align="left"><p>表示的设备</p></td>
<td align="left"><p>驱动程序对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-file-object.md" data-raw-source="[File object](framework-file-object.md)">文件对象</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile" data-raw-source="[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)">IWDFFile</a></p></td>
<td align="left"><p>表示一个文件</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p></p>
否，如果创建的框架;是的如果创建的驱动程序</td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-interrupt-object.md" data-raw-source="[Interrupt object](framework-interrupt-object.md)">中断对象</a></p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfinterrupt" data-raw-source="[IWDFInterrupt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfinterrupt)">IWDFInterrupt</a></td>
<td align="left"><p>表示中断</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-queue-object.md" data-raw-source="[Queue object](framework-i-o-queue-object.md)">队列对象</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfioqueue" data-raw-source="[IWDFIoQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfioqueue)">IWDFIoQueue</a></p></td>
<td align="left"><p>表示接收的 I/O 请求的 I/O 队列</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-i-o-request-object.md" data-raw-source="[Request object](framework-i-o-request-object.md)">请求对象</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest" data-raw-source="[IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest)">IWDFIoRequest</a></p></td>
<td align="left"><p>表示的 I/O 请求</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p></p>
否，如果创建的框架;是的如果创建的驱动程序</td>
<td align="left"><p></p>
否，如果创建的框架 （例如，重定向请求）;是的如果创建的驱动程序</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-target-object.md" data-raw-source="[Target object](framework-i-o-target-object.md)">目标对象</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget" data-raw-source="[IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget)">IWDFIoTarget</a></p></td>
<td align="left"><p>表示另一个驱动程序将发送到请求的驱动程序</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p></p>
否，默认目标;是的对于所有其他目标</td>
</tr>
<tr class="even">
<td align="left"><p>USB 设备对象</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice" data-raw-source="[IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)">IWDFUsbTargetDevice</a></p></td>
<td align="left"><p>表示连接到 USB 设备</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是 （请参阅目标对象）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USB 管道对象</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe" data-raw-source="[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)">IWDFUsbTargetPipe</a></p></td>
<td align="left"><p>表示一个 USB 设备管道</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是 （请参阅目标对象）</p></td>
</tr>
<tr class="even">
<td align="left"><p>USB 接口对象</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)">IWDFUsbInterface</a></p></td>
<td align="left"><p>表示一个 USB 设备接口</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是 （请参阅目标对象）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-base-object.md" data-raw-source="[Base object](framework-base-object.md)">基对象</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject" data-raw-source="[IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject)">IWDFObject</a></p></td>
<td align="left"><p>表示常规的基对象</p></td>
<td align="left"><p>驱动程序对象</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是的如果创建的驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-memory-object.md" data-raw-source="[Memory object](framework-memory-object.md)">内存对象</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[IWDFMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)">IWDFMemory</a></p></td>
<td align="left"><p>表示内存对象</p></td>
<td align="left"><p>驱动程序对象</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p></p>
否，如果创建的框架;是的如果创建的驱动程序</td>
</tr>
</tbody>
</table>

 

 

 





