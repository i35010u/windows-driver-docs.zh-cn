---
title: 指定回调同步模式
description: 指定回调同步模式
ms.assetid: 3e041493-1095-47cb-b9a7-879a4cf1bd2e
keywords:
- 回调同步 WDK UMDF
- 同步 WDK UMDF
- 队列回调函数 WDK UMDF
- 回调函数 WDK UMDF
- I/O 队列 WDK UMDF
- 锁定 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa43943f6925481bf4527a58da4266dbf3444a8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376182"
---
# <a name="specifying-a-callback-synchronization-mode"></a>指定回调同步模式


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

该驱动程序可以指定框架如何调用其回调函数。 该驱动程序指定同步 （或锁定） 的调用之前的设备模式[ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法创建[设备对象](framework-device-object.md)设备. 若要指定同步模式下，该驱动程序应调用[ **IWDFDeviceInitialize::SetLockingConstraint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)方法。 驱动程序收到一个指向[IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)接口时其[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)调用方法以将设备添加到系统。

该驱动程序可以指定以下值之一从 WDF\_回调\_约束中的枚举类型*LockType*参数的**IWDFDeviceInitialize::SetLockingConstraint**确定锁定模式。 约束 （或锁定） 指定的类型取决于硬件设备可以利用对多少并行处理和多大的驱动程序可以处理。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>无</strong>(0)</p></td>
<td align="left"><p>指示已同步到驱动程序没有回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfDeviceLevel</strong> (1)</p></td>
<td align="left"><p>指示已同步到驱动程序的所有队列的回调函数。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  如果驱动程序不会调用**IWDFDeviceInitialize::SetLockingConstraint**若要指定一个值，框架将设置此属性设置为默认值**WdfDeviceLevel**.

 

约束仅适用于队列回调函数而不适用于插即用 (PnP) 和电源管理回调函数。 队列回调函数包括：

-   自动调度回调函数，如[ **IQueueCallbackRead::OnRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackread-onread)并[ **IQueueCallbackWrite::OnWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)。 有关详细信息，请参阅[I/O 队列事件回调函数](i-o-queue-event-callback-functions.md)。

-   队列状态将更改回调函数，例如， [ **IQueueCallbackStateChange::OnStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackstatechange-onstatechange)。

-   例如，请求取消回调函数[ **IRequestCallbackCancel::OnCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel)。

-   文件清理并关闭回调函数，如[ **IFileCallbackCleanup::OnCleanupFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)并[ **IFileCallbackClose::OnCloseFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile).

请求完成回调函数 ([**IRequestCallbackRequestCompletion::OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)) 都不队列是回调函数。 因此，它们不会同步。

 

 





