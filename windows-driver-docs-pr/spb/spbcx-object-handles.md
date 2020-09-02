---
title: SpbCx 对象句柄
description: 本主题介绍为 SPB 框架扩展 (SpbCx) 库定义的对象句柄。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ebcd9644ad26a7d7f8ced3d76ff021cb85ecec6c
ms.sourcegitcommit: c766ab74e32eb44795cbbd1a4f352d3a6a9adc14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89389543"
---
# <a name="spbcx-object-handles"></a>SpbCx 对象句柄

本主题介绍为 SPB 框架扩展 (SpbCx) 库定义的对象句柄。

此外，SerCx2 DDI 使用内核模式驱动程序框架所定义的两个泛型对象句柄类型 WDFDEVICE 和 WDFREQUEST (KMDF) 。
有关框架句柄类型的详细信息，请参阅 [框架对象的摘要](../wdf/summary-of-framework-objects.md)。

本主题介绍下列对象句柄：

* [SPBREQUEST 对象句柄](#spbrequest-object-handle)
* [SPBTARGET 对象句柄](#spbtarget-object-handle)

标头： Spbcx

## <a name="spbrequest-object-handle"></a>SPBREQUEST 对象句柄

**SPBREQUEST**对象句柄表示在总线上颁发给目标设备的 i/o 请求。

```cpp
DECLARE_HANDLE(SPBREQUEST)
```

**SPBREQUEST**对象类派生自**WDFREQUEST**对象类，该类表示由 i/o 管理器调度的 i/o 请求。
因此，采用**WDFREQUEST**句柄值作为参数的**WdfRequestXxx**方法接受**SPBREQUEST**句柄值作为有效参数值。
有关这些方法的详细信息，请参阅 [框架请求对象](../wdf/framework-request-objects.md)。

但是，某些 SpbCx 方法和回调函数特别需要 **SPBREQUEST** 句柄作为参数。
对于这种参数，请将不是**SPBREQUEST**句柄的**WDFREQUEST**句柄替换为错误。

例如， [SpbRequestGetTransferParameters](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters) 方法采用 **SPBREQUEST** 句柄作为参数。
为此，对于此参数，不是也是**SPBREQUEST**句柄的**WDFREQUEST**句柄是一个错误。
此要求的原因是 **SPBREQUEST** 对象必须存储其他特定于 SPB 的状态信息，以支持 [i/o 传输序列](./i-o-transfer-sequences.md)。
**WDFREQUEST**基对象类不提供此支持。

在设备初始化期间，你的 SPB 控制器驱动程序可以通过调用[SpbControllerSetRequestAttributes](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetrequestattributes)方法将每个请求的上下文分配给**SPBREQUEST**句柄。
  
## <a name="spbtarget-object-handle"></a>SPBTARGET 对象句柄

**SPBTARGET**对象句柄标识从客户端 (外围设备驱动程序) 到总线上可寻址端口或外围设备的逻辑连接。

   ```cpp
   DECLARE_HANDLE(SPBTARGET)
   ```

对于 I<sup>2</sup>C 总线， **SPBTARGET** 句柄对应于特定设备地址。  
对于 SPI 总线， **SPBTARGET** 句柄对应于设备-选择行。

通常， **SPBTARGET** 对象是从 [EvtSpbTargetConnect](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect) 事件回调的开头开始，并通过相应的 [EvtSpbTargetDisconnect](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_disconnect) 事件回调结束。 但是，如果 SPB 控制器驱动程序对**SPBTARGET**对象使用其他引用来防止在处理目标的 i/o 请求过程中意外消失对象，则**SPBTARGET**对象的生存期可能超出第二次回调的生存期。

SPB 控制器驱动程序为 SPB 控制器设备执行所有硬件特定的操作。
当客户端发送 [IRP_MJ_CREATE](../ifs/irp-mj-create.md) 请求以打开与总线上的目标的连接时，使用 spb framework 扩展 (SpbCx) 管理控制器驱动程序的 i/o 队列，并通过调用此驱动程序的 [EvtSpbTargetConnect](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect) 回调函数将此请求传递到 SPB 控制器驱动程序。
此函数的此 _Target_ 参数是 **SPBTARGET** 句柄。
函数可以使用此句柄来检索特定于连接的资源信息 (例如，从 PnP 管理器) 设备地址。
当客户端发送 [IRP_MJ_CLOSE](../kernel/irp-mj-close.md) 请求关闭连接时，SpbCx 会将此请求传递给 SPB 控制器驱动程序的 [EvtSpbTargetDisconnect](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_disconnect) 回调函数，这将释放这些资源。

### <a name="exclusive-mode-access"></a>独占模式访问

客户端具有专用模式来访问目标设备。 一次只能有一个客户端与特定目标设备建立连接。
SpbCx 可确保总线上的目标设备地址只存在一个 **SPBTARGET** 句柄。
此限制是必需的，因为 SpbCx 不支持将两个或更多客户端发送到目标设备的 i/o 请求交叉。
如果目标设备必须能够接收来自多个客户端的请求，则此设备需要 MUX 驱动程序（独立于控制器驱动程序），这些驱动程序可以正确地交错请求的操作。

### <a name="interoperability-with-kmdf"></a>与 KMDF 的互操作性

SpbCx 定义的 [SerCx2 驱动程序支持方法](/windows-hardware/drivers/ddi/index) 和 [SpbCx 事件回调函数](/previous-versions/hh450911(v=vs.85)) 使用 **SPBTARGET** 句柄来表示与总线上目标设备的开放连接。
但是，控制器驱动程序通常必须调用需要 WDFFILEOBJECT 处理的 KMDF 方法，而不是 **SPBTARGET** 句柄来指定目标设备。

**SPBTARGET**对象类似于 WDFFILEOBJECT 对象。 但是， **SPBTARGET** 对象包含其他特定于 SPB 的信息。
例如，在处理 [IOCTL_SPB_EXECUTE_SEQUENCE](https://msdn.microsoft.com/library/windows/hardware/hh450857) i/o 控制请求的过程中，目标设备的 **SPBTARGET** 对象跟踪 [i/o 传输序列](./i-o-transfer-sequences.md)中传输的状态。

为获取目标的 WDFFILEOBJECT 句柄，SPB 控制器驱动程序将调用 [SpbTargetGetFileObject](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetfileobject) 方法。
此方法接受作为输入参数、打开目标设备的 **SPBTARGET** 句柄，并将相应的 WDFFILEOBJECT 句柄返回到此目标。

根据 KMDF 约定，SPB 控制器驱动程序可以将其自己的上下文附加到目标设备的 **SPBTARGET** 对象，此上下文可以包括关联的 [EvtCleanupCallback](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 和 [EvtDestroyCallback](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy) 回调函数。
SPB 控制器驱动程序使用此上下文跟踪特定于控制器驱动程序和目标设备的信息。
此外，此驱动程序还可以创建 **SPBTARGET** 对象的子对象，例如计时器、dpc，或根据需要、i/o 请求和 i/o 队列。

## <a name="related-topics"></a>相关主题

[EvtCleanupCallback](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)

[EvtDestroyCallback](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)

[EvtSpbTargetConnect](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect)

[EvtSpbTargetDisconnect](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_disconnect)

[框架请求对象](../wdf/framework-request-objects.md)

[I/o 传输顺序](./i-o-transfer-sequences.md)

[IOCTL_SPB_EXECUTE_SEQUENCE](https://msdn.microsoft.com/library/windows/hardware/hh450857)

[IRP_MJ_CLOSE](../kernel/irp-mj-close.md)

[IRP_MJ_CREATE](../ifs/irp-mj-create.md)

[SerCx2 驱动程序支持方法](/windows-hardware/drivers/ddi/index)

[SpbControllerSetRequestAttributes](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetrequestattributes)

[SpbCx 事件回调函数](/previous-versions/hh450911(v=vs.85))

[SpbRequestGetTransferParameters](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters)

[SpbTargetGetFileObject](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetfileobject)

[框架对象摘要](../wdf/summary-of-framework-objects.md)