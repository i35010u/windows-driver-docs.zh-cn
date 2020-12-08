---
title: 使用 __sdv_save_adapter_context 跟踪适配器上下文字段
description: 使用 __sdv_save_adapter_context 跟踪适配器上下文字段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ad2a1dd319e5a869a1457e25537a1ce672f7c8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840771"
---
# <a name="using-__sdv_save_adapter_context-to-track-adapter-context-fields"></a>使用 \_ \_ sdv \_ 保存 \_ 适配器 \_ 上下文跟踪适配器上下文字段


当 NDIS 调用微型端口驱动程序的 *MiniportInitializeEx* 回调函数以初始化微型端口适配器时，驱动程序会创建自己的内部数据结构来表示微型端口适配器。 驱动程序使用此结构（称为 *微型端口适配器上下文*）来维护设备特定的状态信息，驱动程序需要此信息来管理微型端口适配器。 驱动程序将此结构的句柄传递到 NDIS。

当 NDIS 调用与微型端口适配器相关的微型端口驱动程序的 *MiniportXxx* 函数之一时，ndis 会将微型端口适配器上下文传递给驱动程序，以确定正确的微型端口适配器。 微型端口适配器上下文由微型端口驱动程序拥有和维护，并且对于 NDIS 和协议驱动程序是不透明的。

由于微型端口适配器上下文在 NDIS 调用之间维护微型端口驱动程序的状态，因此 (SDV) 的静态驱动程序验证程序必须能够识别指向此结构的指针。 若要使 SDV 能够跟踪微型端口驱动程序的状态，必须使用 **\_ \_ SDV \_ 保存 \_ 适配器 \_ 上下文** 函数将该句柄保存到微型端口适配器上下文。

**\_ \_ Sdv \_ 保存 \_ 适配器 \_ 上下文** 函数具有以下语法：

```
__sdv_save_adapter_context( &adapter_context ) 
```

其中，适配器 \_ 上下文是微型端口驱动程序定义的微型端口适配器上下文的句柄。 只应在微型端口驱动程序的上下文中调用此函数一次。

**\_ \_ Sdv \_ 保存 \_ 适配器 \_ 上下文** 函数仅由静态分析工具使用。 编译器将忽略此函数。

下面的代码示例演示何时调用 \_ \_ sdv \_ 保存 \_ 适配器 \_ 上下文，以及 sdv 如何在 *微型端口适配器上下文* 中跟踪信息。

下面的代码示例显示了小型端口适配器上下文示例结构 MP 适配器的简化版本 \_ 。

```
typedef struct _MP_ADAPTER
{
    NDIS_HANDLE             AdapterHandle;

    BOOLEAN                 InterruptRegistered;
    NDIS_HANDLE             InterruptHandle;

    /* ..................... */

} MP_ADAPTER, *PMP_ADAPTER;
```

在执行 *MiniportInitializeEx* 的过程中，将为 MP \_ 全名结构分配内存。 紧跟在内存分配之后，将调用 **\_ \_ sdv \_ 保存 \_ 适配器 \_ 上下文**。

如果有指向微型端口适配器上下文结构的有效指针，则必须立即调用 **\_ \_ sdv \_ 保存 \_ 适配器 \_ 上下文** 函数。

```
NDIS_STATUS 
MPInitialize(
    IN  NDIS_HANDLE                        MiniportAdapterHandle,
    IN  NDIS_HANDLE                        MiniportDriverContext,
    IN  PNDIS_MINIPORT_INIT_PARAMETERS     MiniportInitParameters
    )
{
    NDIS_STATUS     Status = NDIS_STATUS_SUCCESS;
    PMP_ADAPTER     pAdapter = NULL;
 
    /* ..................... */
 
    do
    {
   // allocate the memory for the AdapterContext
        pAdapter = NdisAllocateMemoryWithTagPriority(
            MiniportAdapterHandle,
            sizeof(MP_ADAPTER),
            NIC_TAG,
            LowPoolPriority
            );

   // save the adapter context, even before we check whether it is NULL or not 
 __sdv_save_adapter_context(&pAdapter);

        if (pAdapter == NULL)
        {
            Status = NDIS_STATUS_RESOURCES;
            break;
        }
 
        NdisZeroMemory(pAdapter, sizeof(MP_ADAPTER));
 
        pAdapter->AdapterHandle = MiniportAdapterHandle;
        pAdapter->PauseState = NicPaused;

   /* ..................... */
```

下面的代码示例演示了 SDV 如何跟踪微型端口适配器上下文中的值。 在此示例中，驱动程序通过调用微型端口提供的函数 *MpRegisterInterrupt* 来注册中断。 如果调用成功，驱动程序会将结果保存到小型端口适配器上下文中 (*pAdapter*) 字段 "InterruptRegistered"。

```
//
// Register the interrupt
   //
        Status = MpRegisterInterrupt(pAdapter);
        if (Status != NDIS_STATUS_SUCCESS)
        {
            break;
        }
 
   // save the value of the result into the AdapterContext
        pAdapter->InterruptRegistered = TRUE;
```

当需要暂停微型端口驱动程序时，NDIS 会通过将句柄传递给微型端口适配器上下文来调用驱动程序的 *MiniportHaltEx* 函数。 由于 SDV 还具有此句柄，因此从前面调用 **\_ \_ SDV \_ 保存 \_ 适配器 \_ 上下文** 时，SDV 可以跟踪 InterruptRegistered 字段的值。

```
VOID MPHalt(
    IN  NDIS_HANDLE             MiniportAdapterContext,
    IN  NDIS_HALT_ACTION        HaltAction
    )
{
    PMP_ADAPTER     pAdapter = (PMP_ADAPTER) MiniportAdapterContext;
 
    /* ..................... */

    if (pAdapter->InterruptRegistered)
    {
        NdisMDeregisterInterruptEx(pAdapter->InterruptHandle);
        pAdapter->InterruptRegistered = FALSE;
    }

/* ..................... */
```

 

 





