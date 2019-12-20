---
title: 指定回调同步模式
description: 指定回调同步模式
ms.assetid: 3e041493-1095-47cb-b9a7-879a4cf1bd2e
keywords:
- 回调同步 WDK UMDF
- 同步 WDK UMDF
- 队列回调函数 WDK UMDF
- 回调函数 WDK UMDF
- I/o 队列 WDK UMDF
- 锁定 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a461ffece59f2890abab078372a938d551b243
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209949"
---
# <a name="specifying-a-callback-synchronization-mode"></a>指定回调同步模式


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

驱动程序可以指定框架如何调用回调函数。 在调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法为设备创建[设备对象](framework-device-object.md)之前，驱动程序为设备指定同步（或锁定）模式。 若要指定同步模式，驱动程序应调用[**IWDFDeviceInitialize：： SetLockingConstraint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)方法。 当调用[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法将设备添加到系统时，驱动程序将收到指向[IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)接口的指针。

驱动程序可以在**IWDFDeviceInitialize：： SetLockingConstraint**的*LockType*参数中的 WDF\_回调\_约束枚举类型中指定以下值之一，以标识锁定模式。 指定的约束（或锁定）的类型取决于硬件设备可以利用的并行度以及驱动程序可以处理的数量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>无</strong>（0）</p></td>
<td align="left"><p>指示不同步对驱动程序的回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfDeviceLevel</strong> （1）</p></td>
<td align="left"><p>指示同步所有队列回调函数到驱动程序中。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   如果驱动程序未调用**IWDFDeviceInitialize：： SetLockingConstraint**来指定值，则框架会将此属性的默认值设置为**WdfDeviceLevel**。

 

约束仅适用于队列回调函数，不适用于即插即用（PnP）和电源管理回调函数。 队列回调函数包括：

-   自动调度回调函数，如， [**IQueueCallbackRead：： OnRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread)和[**IQueueCallbackWrite：： OnWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)。 有关详细信息，请参阅[I/o 队列事件回调函数](i-o-queue-event-callback-functions.md)。

-   队列状态更改回调函数，如， [**IQueueCallbackStateChange：： OnStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackstatechange-onstatechange)。

-   请求取消回调函数，如， [**IRequestCallbackCancel：： OnCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel)。

-   文件清理和关闭回调函数，如， [**IFileCallbackCleanup：： OnCleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)和[**IFileCallbackClose：： OnCloseFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)。

请求完成回调函数（[**IRequestCallbackRequestCompletion：： OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)）不是队列回调函数。 因此，它们不会同步。

 

 





