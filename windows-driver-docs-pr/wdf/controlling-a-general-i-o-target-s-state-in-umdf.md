---
title: 在 UMDF 中控制常规 I/O 目标的状态
description: 在 UMDF 中控制常规 I/O 目标的状态
ms.assetid: 479487b2-5ce5-4522-b195-58ee50d210b6
keywords:
- 一般 i/o 目标是 WDK UMDF，状态
- 已启动 i/o 目标状态 WDK UMDF
- 已停止 i/o 目标状态 WDK UMDF
- 已关闭，用于查询-删除状态 WDK UMDF
- 已关闭 i/o 目标状态 WDK UMDF
- 已删除 i/o 目标状态 WDK UMDF
- 本地 i/o 目标 WDK UMDF
- 远程 i/o 目标 WDK UMDF
- 停止 i/o 目标
- 重新启动 i/o 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f51efc9445a154592db73216cc495b858565f1e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843643"
---
# <a name="controlling-a-general-io-targets-state-in-umdf"></a>在 UMDF 中控制常规 I/O 目标的状态


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架定义一般 i/o 目标的以下状态：

<a href="" id="started"></a>**首先**  
I/o 目标已打开（即，可用于 UMDF 驱动程序），驱动程序可向其发送 i/o 请求。 框架将请求传递给相应的驱动程序。

<a href="" id="stopped"></a>**停下**  
I/o 目标处于打开状态，但是 UMDF 驱动程序无法向 i/o 目标发送 i/o 请求，除非该驱动程序将 WDF\_请求\_发送\_选项\_在对[**IWDFIoRequest：： send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)方法的调用中将\_目标\_状态标志忽略到*Flags*参数。

框架停止向相应的驱动程序传递请求。

<a href="" id="closed-for-query-remove-------"></a>**已关闭以进行查询-删除**   
由于 i/o 目标可能很快会被删除，因此该目标已暂时关闭。

<a href="" id="closed"></a>**闭**  
I/o 目标已关闭，无法启动或停止。

<a href="" id="deleted"></a>**删除**  
已删除 i/o 目标的设备。

[**WDF\_IO\_TARGET\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)枚举定义表示这些状态的值。

### <a name="local-io-target-states"></a>本地 i/o 目标状态

框架将自动打开并启动本地 i/o 目标。

如有必要，驱动程序可以调用[**IWDFIoTargetStateManagement：： Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)来暂时停止本地 i/o 目标并调用[**IWDFIoTargetStateManagement：： Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)来重新启动它。 例如，如果检测到临时错误情况，驱动程序可能会停止本地 i/o 目标，如果更正错误条件，则重新启动 i/o 目标。

如果删除了本地 i/o 目标设备，框架将自动停止并关闭 i/o 目标，并[取消](canceling-i-o-requests.md)目标队列中的所有 i/o 请求。 框架通过调用设备对象事件回调函数通知驱动程序设备不再可用。 有关这些回调函数的详细信息，请参阅[UMDF 中的 PnP 和电源管理方案](pnp-and-power-management-scenarios-in-umdf.md)。

驱动程序可以调用[**IWDFIoTargetStateManagement：： GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)以获取本地 i/o 目标的当前状态。

### <a name="remote-io-target-states"></a>远程 i/o 目标状态

驱动程序必须调用[**IWDFRemoteTarget：： OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)或[**IWDFRemoteTarget：： OpenRemoteInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface)来打开远程 i/o 目标。 当驱动程序打开远程 i/o 目标时，框架会自动启动 i/o 目标。

如有必要，驱动程序可以调用[**IWDFRemoteTarget：： Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-stop)来暂时停止远程 i/o 目标并调用[**IWDFRemoteTarget：： Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-start)来重新启动它。

如果删除了远程 i/o 目标设备，则框架将自动停止并关闭 i/o 目标，并取消目标队列中的所有 i/o 请求，除非驱动程序注册以下事件回调函数：

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetqueryremove--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetQueryRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetqueryremove)  
通知驱动程序远程 i/o 目标设备可能已被删除。 如果希望驱动程序允许删除设备，则驱动程序必须调用[**IWDFRemoteTarget：： CloseForQueryRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-closeforqueryremove) 。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetremovecomplete--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetRemoveComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetremovecomplete)  
通知驱动程序远程 i/o 目标的设备已被删除。 此回调函数必须调用[**IWDFRemoteTarget：： Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-close)。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetremovecanceled--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetRemoveCanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetremovecanceled)  
通知驱动程序删除远程 i/o 目标设备的尝试已被取消。 如果希望驱动程序继续使用目标，则驱动程序必须调用[**IWDFRemoteTarget：：重新打开**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-reopen)。 通常，驱动程序调用从**OnRemoteTargetRemoveCanceled**回调函数中**重新打开**，但**重新打开**可以在**OnRemoteTargetRemoveCanceled**返回后调用。

驱动程序可以调用[**IWDFRemoteTarget：： GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-getstate)以获取远程 i/o 目标的当前状态。

 

 





