---
title: WDF 缓冲区指针的 WDM 等效项
description: WDF 缓冲区指针的 WDM 等效项
ms.assetid: 7923A3CA-479A-4C7D-B428-F57C9701906E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 070361e6d9df0b7ac8a17c533eecc5cf93cd07b4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186251"
---
# <a name="wdm-equivalents-for-wdf-buffer-pointers"></a>WDF 缓冲区指针的 WDM 等效项


内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序使用以下方法来检索缓冲和直接 i/o 的 i/o 缓冲区。 除非另行指定，否则这些方法同时适用于 KMDF 和 UMDF。

-   [**WdfRequestRetrieveOutputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)
-   [**WdfRequestRetrieveOutputWdmMdl (KMDF 仅) **](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)
-   [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)
-   [**WdfRequestRetrieveInputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)
-   [**WdfRequestRetrieveInputWdmMdl (KMDF 仅) **](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)
-   [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)

下表描述了对于 \_ \_ 缓冲和直接 i/o，为 irp mj 读取、irp \_ MJ \_ 写入和 irp \_ mj \_ 设备 \_ 控制请求返回的内容。 对 i/o 的请求都需要特殊处理，因为在请求用户模式进程的上下文中运行时，驱动程序必须检索缓冲区。

## <a name="buffers-for-irp_mj_read-requests"></a><a href="" id="read"></a>IRP \_ MJ \_ 读取请求的缓冲区


若要检索读取请求的缓冲区，KMDF 驱动程序将调用 **WdfRequestRetrieveOutput**_Xxx_ 方法之一。 其中每个方法返回的缓冲区会有所不同，具体取决于驱动程序是执行缓冲还是直接 i/o。 下表描述了 WDM 术语中每个方法所返回的指针。

| 函数                                                                             | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveOutputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp- &gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) (**Irp- &gt; MdlAddress**)                                                                                                           |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF 仅) **](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | 为 **Irp &gt;AssociatedIrp.SystemBuffer** 生成 (MDL) 的内存描述符列表，并返回 mdl。                                           | **Irp- &gt; MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | 返回 WDFMEMORY 对象。 对此对象调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 以获取 **Irp &gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 对此对象调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 以获取 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) (**Irp- &gt; MdlAddress**) 。 |

 

## <a name="buffers-for-irp_mj_write-requests"></a><a href="" id="write"></a>IRP \_ MJ \_ 写入请求的缓冲区


若要检索写入请求的缓冲区，KMDF 驱动程序将调用 **WdfRequestRetrieveInput**_Xxx_ 方法之一。 其中每个方法返回的缓冲区会有所不同，具体取决于驱动程序是执行缓冲还是直接 i/o。 下表描述了 WDM 术语中每个方法所返回的指针。

| 函数                                                                           | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)             | **Irp- &gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) (**Irp- &gt; MdlAddress**)                                                                                                           |
| [**WdfRequestRetrieveInputWdmMdl (KMDF 仅) **](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) | 为 **Irp &gt;AssociatedIrp.SysTEMBUFFER** 生成 MDL 并返回 mdl。                                                                   | **Irp- &gt; MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)             | 返回 WDFMEMORY 对象。 对此对象调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 以获取 **Irp &gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 对此对象调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 以获取 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) (**Irp- &gt; MdlAddress**) 。 |

 

## <a name="buffers-for-irp_mj_device_control-requests"></a><a href="" id="device-control"></a>IRP \_ MJ \_ 设备 \_ 控制请求的缓冲区


若要检索设备 i/o 控制请求的缓冲区，KMDF 驱动程序需要调用 **WdfRequestRetrieveInputXxx** 或 **WdfRequestRetrieveOutputXxx** 方法。 其中每个方法返回的缓冲区会有所不同，具体取决于驱动程序是执行 [缓冲还是直接](./accessing-data-buffers-in-wdf-drivers.md)i/o，如下表所示：

| 函数                                                                             | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)               | **Irp- &gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) (**Irp- &gt; MdlAddress**)                                                                                                           |
| [**WdfRequestRetrieveInputWdmMdl (KMDF 仅) **](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)   | 为 **Irp &gt;AssociatedIrp.SysTEMBUFFER** 生成 MDL 并返回 mdl。                                                                   | 为 **Irp &gt;AssociatedIrp.SysTEMBUFFER** 生成 MDL 并返回 mdl。                                                                                                                             |
| [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)               | 返回 WDFMEMORY 对象。 对此对象调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 以获取 **Irp &gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 对此对象调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 以获取 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) (**Irp- &gt; MdlAddress**) 。 |
| [**WdfRequestRetrieveOutputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp- &gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) (**Irp- &gt; MdlAddress**)                                                                                                           |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF 仅) **](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | 为 **Irp &gt;AssociatedIrp.SystemBuffer** 生成 (MDL) 的内存描述符列表，并返回 mdl。                                           | **Irp- &gt; MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | 返回 WDFMEMORY 对象。 对此对象调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 以获取 **Irp &gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 对此对象调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 以获取 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) (**Irp- &gt; MdlAddress**) 。 |

 

 

