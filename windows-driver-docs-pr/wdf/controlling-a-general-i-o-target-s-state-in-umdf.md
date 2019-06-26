---
title: 在 UMDF 中控制常规 I/O 目标的状态
description: 在 UMDF 中控制常规 I/O 目标的状态
ms.assetid: 479487b2-5ce5-4522-b195-58ee50d210b6
keywords:
- 常规 I/O 面向 WDK UMDF，状态
- 已启动 I/O 目标状态 WDK UMDF
- 停止 I/O 目标状态 WDK UMDF
- 已关闭的查询删除状态 WDK UMDF
- 已关闭的 I/O 目标状态 WDK UMDF
- 已删除的 I/O 目标状态 WDK UMDF
- 本地 I/O 面向 WDK UMDF
- 远程 I/O 面向 WDK UMDF
- 正在停止 I/O 目标
- 重新启动 I/O 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d1368de4df4f2f559e3405dc901d6c4ead9e474
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382878"
---
# <a name="controlling-a-general-io-targets-state-in-umdf"></a>在 UMDF 中控制常规 I/O 目标的状态


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

该框架定义常规 I/O 目标的以下的状态：

<a href="" id="started"></a>**已启动**  
I/O 目标处于打开状态 (即，供 UMDF 驱动程序) 和驱动程序可以向其发送的 I/O 请求。 框架将请求传递给相应的驱动程序。

<a href="" id="stopped"></a>**已停止**  
I/O 目标处于打开状态，但除非驱动程序通过了 WDF UMDF 驱动程序无法将输入/输出请求发送到 I/O 目标\_请求\_发送\_选项\_忽略\_目标\_状态标志*标志*调用中的参数[ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)方法。

该框架会停止将请求传递到相应的驱动程序。

<a href="" id="closed-for-query-remove-------"></a>**已关闭的查询删除**   
I/O 目标已暂时关闭，因为可能很快就会删除其设备。

<a href="" id="closed"></a>**关闭**  
I/O 目标已关闭，无法启动或停止。

<a href="" id="deleted"></a>**已删除**  
已删除 I/O 目标设备。

[ **WDF\_IO\_目标\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)枚举定义表示这些状态的值。

### <a name="local-io-target-states"></a>本地 I/O 目标状态

框架会自动打开，并启动本地 I/O 目标。

如果有必要，则该驱动程序可以调用[ **IWDFIoTargetStateManagement::Stop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)若要暂时停止本地 I/O 目标和调用[ **IWDFIoTargetStateManagement::Start** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)来重新启动它。 例如，驱动程序可能会停止本地 I/O 目标，如果它检测到临时错误条件，然后重新启动 I/O 目标，如果错误条件，则在更正。

如果移除本地 I/O 目标设备后，框架会自动停止并关闭 I/O 目标和[取消](canceling-i-o-requests.md)目标的队列中的所有 I/O 请求。 该框架会通知驱动程序，该设备不可再通过调用回调函数的设备对象事件。 有关这些回调函数的详细信息，请参阅[PnP 和电源管理方案，在 UMDF](pnp-and-power-management-scenarios-in-umdf.md)。

驱动程序可以调用[ **IWDFIoTargetStateManagement::GetState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)若要获取本地 I/O 目标的当前状态。

### <a name="remote-io-target-states"></a>远程 I/O 目标状态

驱动程序必须调用[ **IWDFRemoteTarget::OpenFileByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)或[ **IWDFRemoteTarget::OpenRemoteInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface)若要打开远程 I/O目标。 当驱动程序打开远程 I/O 目标时，框架会自动启动 I/O 目标。

如果有必要，则该驱动程序可以调用[ **IWDFRemoteTarget::Stop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-stop)若要暂时停止远程 I/O 目标并调用[ **IWDFRemoteTarget::Start** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-start)来重新启动它。

如果移除远程 I/O 目标设备后，框架会自动停止和关闭 I/O 目标和取消的目标队列中的所有 I/O 请求，除非该驱动程序将注册以下事件回调函数：

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetqueryremove--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetQueryRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetqueryremove)  
告知驱动程序可能会删除远程 I/O 目标设备。 您的驱动程序必须调用[ **IWDFRemoteTarget::CloseForQueryRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-closeforqueryremove)如果你想要允许删除该设备的驱动程序。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetremovecomplete--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetRemoveComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetremovecomplete)  
告知驱动程序已删除远程 I/O 目标设备。 必须调用此回调函数[ **IWDFRemoteTarget::Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-close)。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetremovecanceled--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetRemoveCanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetremovecanceled)  
告知驱动程序已取消尝试删除远程 I/O 目标设备。 如果你想要继续使用目标的驱动程序，该驱动程序必须调用[ **IWDFRemoteTarget::Reopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-reopen)。 通常情况下，驱动程序调用**重新打开**内**OnRemoteTargetRemoveCanceled**回调函数，但**重新打开**可以改为调用后**OnRemoteTargetRemoveCanceled**返回。

驱动程序可以调用[ **IWDFRemoteTarget::GetState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-getstate)获取远程 I/O 目标的当前状态。

 

 





