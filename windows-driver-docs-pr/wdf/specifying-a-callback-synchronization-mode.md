---
title: 指定回调同步模式
description: 指定回调同步模式
keywords:
- 回调同步 WDK UMDF
- 同步 WDK UMDF
- 队列回调函数 WDK UMDF
- 回调函数 WDK UMDF
- I/o 队列 WDK UMDF
- 锁定 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ee6d4f686f00da6f94e7e32da7863229becab92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821153"
---
# <a name="specifying-a-callback-synchronization-mode"></a>指定回调同步模式


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

驱动程序可以指定框架如何调用回调函数。 在调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice) 方法为设备创建 [设备对象](framework-device-object.md) 之前，驱动程序为设备指定同步 (或锁定) 模式。 若要指定同步模式，驱动程序应调用 [**IWDFDeviceInitialize：： SetLockingConstraint**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint) 方法。 当调用 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法将设备添加到系统时，驱动程序将收到指向 [IWDFDeviceInitialize](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)接口的指针。

驱动程序可以 \_ \_ 在 **IWDFDeviceInitialize：： SetLockingConstraint** 的 *LockType* 参数中的 WDF 回调约束枚举类型中指定以下值之一，以标识锁定模式。  (或锁定) 指定的约束类型取决于硬件设备可以利用的并行度以及驱动程序可以处理的数量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>无</strong> (0) </p></td>
<td align="left"><p>指示不同步对驱动程序的回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfDeviceLevel</strong> (1) </p></td>
<td align="left"><p>指示同步所有队列回调函数到驱动程序中。</p></td>
</tr>
</tbody>
</table>

 

**注意**   如果驱动程序未调用 **IWDFDeviceInitialize：： SetLockingConstraint** 来指定值，则框架会将此属性的默认值设置为 **WdfDeviceLevel**。

 

约束仅适用于队列回调函数，不适用于即插即用 (PnP) 和电源管理回调函数。 队列回调函数包括：

-   自动调度回调函数，如， [**IQueueCallbackRead：： OnRead**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread) 和 [**IQueueCallbackWrite：： OnWrite**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)。 有关详细信息，请参阅 [I/o 队列事件回调函数](i-o-queue-event-callback-functions.md)。

-   队列状态更改回调函数，如， [**IQueueCallbackStateChange：： OnStateChange**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackstatechange-onstatechange)。

-   请求取消回调函数，如， [**IRequestCallbackCancel：： OnCancel**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel)。

-   文件清理和关闭回调函数，如， [**IFileCallbackCleanup：： OnCleanupFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile) 和 [**IFileCallbackClose：： OnCloseFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)。

请求完成回调函数 ([**IRequestCallbackRequestCompletion：： OnCompletion**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)) 不是队列回调函数。 因此，它们不会同步。

 

