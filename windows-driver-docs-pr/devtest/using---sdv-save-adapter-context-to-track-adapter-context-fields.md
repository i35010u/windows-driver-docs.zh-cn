---
title: 使用 __sdv_save_adapter_context 跟踪适配器上下文字段
description: 使用 __sdv_save_adapter_context 跟踪适配器上下文字段
ms.assetid: b43d7ef5-0464-4e07-a5ec-9d7d8a55479e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05980287e270604da7d57d9eab5e8cdbbf8a1a7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341653"
---
# <a name="using-sdvsaveadaptercontext-to-track-adapter-context-fields"></a>使用\_ \_sdv\_保存\_适配器\_跟踪适配器上下文字段的上下文


当 NDIS 调用微型端口驱动程序*MiniportInitializeEx*回调函数来初始化的微型端口适配器，该驱动程序将创建其自己的内部数据结构来表示微型端口适配器。 驱动程序将使用此结构称为*微型端口适配器上下文*、 维护驱动程序需要以管理微型端口适配器的特定于设备的状态信息。 该驱动程序将一个句柄传递给到 NDIS 此结构。

当 NDIS 调用微型端口驱动程序之一*MiniportXxx* NDIS 的微型端口适配器上下文传递标识正确的微型端口适配器添加到驱动程序微型端口适配器与相关的函数。 拥有和维护的微型端口驱动程序微型端口适配器上下文表示到 NDIS 和协议驱动程序不透明。

微型端口适配器上下文维护 NDIS 调用之间的微型端口驱动程序的状态，因为 Static Driver Verifier (SDV) 必须能够确定指向此结构的指针。 若要启用 SDV 来跟踪状态的微型端口驱动程序，您必须使用将保存句柄到微型端口适配器上下文 **\_ \_sdv\_保存\_适配器\_上下文**函数。

**\_\_Sdv\_保存\_适配器\_上下文** 函数具有以下语法：

```
__sdv_save_adapter_context( &adapter_context ) 
```

其中适配器\_上下文是由微型端口驱动程序定义的微型端口适配器上下文的句柄。 此函数应调用一次只能微型端口驱动程序的上下文中。

**\_\_Sdv\_保存\_适配器\_上下文** 函数只能使用由静态分析工具。 编译器将忽略此函数。

下面的代码示例显示了何时调用\_ \_sdv\_保存\_适配器\_上下文和 SDV 如何将跟踪中的信息*微型端口适配器上下文*。

下面的代码示例显示了一个简化的版的微型端口适配器上下文示例结构 MP\_适配器。

```
typedef struct _MP_ADAPTER
{
    NDIS_HANDLE             AdapterHandle;

    BOOLEAN                 InterruptRegistered;
    NDIS_HANDLE             InterruptHandle;

    /* ..................... */

} MP_ADAPTER, *PMP_ADAPTER;
```

在执行期间*MiniportInitializeEx*，将管理包的内存\_全名结构分配。 内存分配，紧跟 **\_ \_sdv\_保存\_适配器\_上下文**调用。

必须调用 **\_ \_sdv\_保存\_适配器\_上下文**函数只要有指向微型端口适配器上下文结构的有效指针。

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

下面的代码示例演示如何 SDV 跟踪微型端口适配器上下文中的值。 在此示例中，该驱动程序中断注册通过调用提供微型端口的函数， *MpRegisterInterrupt*。 如果调用成功，驱动程序会将结果保存到微型端口适配器上下文 (*pAdapter*) 字段中，InterruptRegistered。

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

NDIS 微型端口驱动程序必须暂停，当调用的驱动程序*MiniportHaltEx*函数通过将该句柄传递给微型端口适配器上下文。 因为 SDV 也具有此句柄，从之前调用 **\_ \_sdv\_保存\_适配器\_上下文**，SDV 可以跟踪 InterruptRegistered 字段的值。

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

 

 





