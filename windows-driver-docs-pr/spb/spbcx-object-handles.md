---
title: SpbCx 对象句柄
description: 本主题介绍存储 framework 扩展 (SpbCx) 库定义的对象句柄。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 89ff2985adbc199650000ce27741c71928dfd94a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519282"
---
# <a name="spbcx-object-handles"></a>SpbCx 对象句柄
本主题介绍存储 framework 扩展 (SpbCx) 库定义的对象句柄。 

此外，SerCx2 DDI 使用两个泛型对象句柄类型、 WDFDEVICE 和 WDFREQUEST，定义由内核模式驱动程序框架 (KMDF)。 有关框架句柄类型的详细信息，请参阅[Framework 对象摘要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)。

本主题介绍以下对象句柄：

* [SPBREQUEST 对象句柄](#SPBREQUEST)
* [SPBTARGET 对象句柄](#SPBTARGET)

标头：Spbcx.h

##  <a name="spbrequest-object-handle"></a>SPBREQUEST 对象句柄
**SPBREQUEST**对象句柄表示颁发到总线上的目标设备的 I/O 请求。

```cpp
DECLARE_HANDLE(SPBREQUEST)
```

**SPBREQUEST**对象类派生自**WDFREQUEST**对象类，该类表示 I/O 管理器调度的 I/O 请求。 因此， **WdfRequestXxx**采用的方法**WDFREQUEST**处理值，因为参数接受**SPBREQUEST**处理作为有效参数值的值。 有关这些方法的详细信息，请参阅[Framework 请求对象](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects)。

但是，某些 SpbCx 方法和回调函数专门要求**SPBREQUEST**句柄作为参数。 对于此类参数，并替换**WDFREQUEST**句柄，也不是**SPBREQUEST**句柄时出错。

例如， [SpbRequestGetTransferParameters](https://msdn.microsoft.com/library/windows/hardware/hh450924)方法采用**SPBREQUEST**处理作为参数。 若要为此参数，提供**WDFREQUEST**句柄，也不是**SPBREQUEST**句柄时出错。 这一要求的原因在于**SPBREQUEST**对象必须存储其他特定于存储的状态信息，以支持[I/O 传输序列](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)。 **WDFREQUEST**基对象类不提供此支持。

设备在初始化期间，您的存储控制器驱动程序可以分配到的每个请求上下文**SPBREQUEST**处理通过调用[SpbControllerSetRequestAttributes](https://msdn.microsoft.com/library/windows/hardware/hh450908)方法。
  
##  <a name="spbtarget-object-handle"></a>SPBTARGET 对象句柄
**SPBTARGET**对象句柄标识从客户端 （外围设备驱动程序） 到可寻址端口或外围设备总线上的逻辑连接。
   
   ```cpp
   DECLARE_HANDLE(SPBTARGET)
   ```
对于 I<sup>2</sup>C 总线**SPBTARGET**句柄对应于特定设备地址。  
有关 SPI 总线**SPBTARGET**句柄对应于设备选择行。

通常情况下， **SPBTARGET**对象从开始处存在[EvtSpbTargetConnect](https://msdn.microsoft.com/library/windows/hardware/hh450818)通过相应的结束事件回调[EvtSpbTargetDisconnect](https://msdn.microsoft.com/library/windows/hardware/hh450820)事件回调。 但是的生存期**SPBTARGET**对象可能会超出第二个回调，如果存储控制器驱动程序采用其他引用**SPBTARGET**对象以防止该对象从意外的目标的 I/O 请求处理过程中逐渐消失。

存储控制器驱动程序执行的存储控制器设备的所有特定于硬件的操作。 当客户端发送[IRP_MJ_CREATE](https://msdn.microsoft.com/library/windows/hardware/ff548630)打开到总线，用于管理控制器驱动程序的 I/O 队列，存储框架扩展 (SpbCx) 上的目标的连接请求将此请求传递到存储控制器驱动程序由调用此驱动程序[EvtSpbTargetConnect](https://msdn.microsoft.com/library/windows/hardware/hh450818)回调函数。 这_目标_此函数的参数**SPBTARGET**处理。 该函数可以使用此句柄来检索特定于连接的资源信息 （例如，设备地址） 从 PnP 管理器。 当客户端发送[IRP_MJ_CLOSE](https://msdn.microsoft.com/library/windows/hardware/ff550720)请求来关闭连接，SpbCx 将此请求传递到存储控制器驱动程序[EvtSpbTargetDisconnect](https://msdn.microsoft.com/library/windows/hardware/hh450820)回调函数，以释放这些资源。

### <a name="exclusive-mode-access"></a>独占模式访问
客户端具有排他模式来访问目标设备。 只有一个客户端可以具有一次连接到特定目标设备。 SpbCx 可确保只有一个**SPBTARGET**总线上的目标设备地址存在句柄。 此限制是必要的因为 SpbCx 不支持交错的两个或多个客户端发送到目标设备的 I/O 请求。 如果目标设备必须能够接收来自多个客户端请求，此设备需要一个 MUX 驱动程序 — 独立于控制器驱动程序 — 的正确可以交错所请求的操作。

### <a name="interoperability-with-kmdf"></a>与 KMDF 互操作性
[SerCx2 驱动程序支持的方法](https://msdn.microsoft.com/library/windows/hardware/dn265323)和[SpbCx 事件回调函数](https://msdn.microsoft.com/library/windows/hardware/hh450911)定义的情况下使用 SpbCx **SPBTARGET**句柄来表示打开的连接目标总线上的设备。 但是，控制器驱动程序通常必须调用 KMDF 方法而不是需要 WDFFILEOBJECT 句柄**SPBTARGET**句柄，以指定目标设备。

**SPBTARGET**对象都类似于 WDFFILEOBJECT 对象。 但是， **SPBTARGET**对象包含特定于存储的其他信息。 例如，在处理期间[IOCTL_SPB_EXECUTE_SEQUENCE](https://msdn.microsoft.com/library/windows/hardware/hh450857) I/O 控制请求**SPBTARGET**对象的目标设备跟踪中传输的状态[I/O传输序列](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)。

若要获取的 WDFFILEOBJECT 句柄的目标存储控制器驱动程序调用[SpbTargetGetFileObject](https://msdn.microsoft.com/library/windows/hardware/hh450927)方法。 作为输入参数，此方法接受**SPBTARGET**句柄的打开目标设备，并返回相应 WDFFILEOBJECT 句柄此目标。

根据 KMDF 约定存储控制器驱动程序可以将附加到其自身的上下文**SPBTARGET**对象的目标设备，并在此上下文可能包括相关联[EvtCleanupCallback](https://msdn.microsoft.com/library/windows/hardware/ff540840)和[EvtDestroyCallback](https://msdn.microsoft.com/library/windows/hardware/ff540841)回调函数。 存储控制器驱动程序使用此上下文跟踪特定于控制器驱动程序和目标设备的信息。 此外，此驱动程序可以创建子对象的**SPBTARGET**对象，例如计时器，dpc 进行标记，或者，如果需要 I/O 请求和 I/O 队列。
 
## <a name="related-topics"></a>相关主题

[EvtCleanupCallback](https://msdn.microsoft.com/library/windows/hardware/ff540840)

[EvtDestroyCallback](https://msdn.microsoft.com/library/windows/hardware/ff540841)

[EvtSpbTargetConnect](https://msdn.microsoft.com/library/windows/hardware/hh450818)

[EvtSpbTargetDisconnect](https://msdn.microsoft.com/library/windows/hardware/hh450820)

[Framework 请求对象](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects)

[I/O 传输序列](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)

[IOCTL_SPB_EXECUTE_SEQUENCE](https://msdn.microsoft.com/library/windows/hardware/hh450857)

[IRP_MJ_CLOSE](https://msdn.microsoft.com/library/windows/hardware/ff550720)

[IRP_MJ_CREATE](https://msdn.microsoft.com/library/windows/hardware/ff548630)

[SerCx2 驱动程序支持的方法](https://msdn.microsoft.com/library/windows/hardware/dn265323)

[SpbControllerSetRequestAttributes](https://msdn.microsoft.com/library/windows/hardware/hh450908)

[SpbCx 事件回调函数](https://msdn.microsoft.com/library/windows/hardware/hh450911)

[SpbRequestGetTransferParameters](https://msdn.microsoft.com/library/windows/hardware/hh450924)

[SpbTargetGetFileObject](https://msdn.microsoft.com/library/windows/hardware/hh450927)

[Framework 对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)



