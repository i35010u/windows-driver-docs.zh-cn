---
title: WDF 缓冲区指针的 WDM 等效项
description: WDF 缓冲区指针的 WDM 等效项
ms.assetid: 7923A3CA-479A-4C7D-B428-F57C9701906E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c2b9a9a11234afa22da5492671e22d01614d5d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354430"
---
# <a name="wdm-equivalents-for-wdf-buffer-pointers"></a>WDF 缓冲区指针的 WDM 等效项


内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序使用以下方法来检索用于缓冲和直接 I/O 的 I/O 缓冲区。 除非另行指定，方法适用于 KMDF 和 UMDF。

-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)
-   [**WdfRequestRetrieveOutputWdmMdl (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)
-   [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)
-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)
-   [**WdfRequestRetrieveInputWdmMdl (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)
-   [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)

下表描述了 IRP 的检索方法返回什么\_MJ\_读取、 IRP\_MJ\_写入和 IRP\_MJ\_设备\_控件请求缓冲和直接 I/O。 既不 I/O 请求需要特殊处理，因为该驱动程序必须在请求的用户模式进程的上下文中运行时检索缓冲区。

## <a href="" id="read"></a>IRP 的缓冲区\_MJ\_读取的请求


若要检索的读取请求的缓冲区，KMDF 驱动程序调用其中一种 **WdfRequestRetrieveOutput * * * Xxx*方法。 缓冲区的每个这些方法返回各不相同，具体取决于驱动程序是否执行缓冲或直接 I/O。 下表描述了每个方法在 WDM 术语中返回的指针。

| 函数                                                                             | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | 为生成内存描述符列表 (MDL) **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)若要获取此对象上**Irp-&gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)若要获取此对象上[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;MdlAddress**)。 |

 

## <a href="" id="write"></a>IRP 的缓冲区\_MJ\_写入请求


若要检索的写入请求的缓冲区，KMDF 驱动程序调用其中一种 **WdfRequestRetrieveInput * * * Xxx*方法。 缓冲区的每个这些方法返回各不相同，具体取决于驱动程序是否执行缓冲或直接 I/O。 下表描述了每个方法在 WDM 术语中返回的指针。

| 函数                                                                           | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) | 生成有关 MDL **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                                                   | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)             | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)若要获取此对象上**Irp-&gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)若要获取此对象上[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;MdlAddress**)。 |

 

## <a href="" id="device-control"></a>IRP 的缓冲区\_MJ\_设备\_控制请求


若要检索设备 I/O 控制请求的缓冲区，KMDF 驱动程序调用任一**WdfRequestRetrieveInputXxx**或**WdfRequestRetrieveOutputXxx**方法。 缓冲区的每个这些方法返回各不相同，具体取决于驱动程序的执行是否[缓冲或直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)下, 表中所示：

| 函数                                                                             | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)               | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)   | 生成有关 MDL **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                                                   | 生成有关 MDL **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                                                                                                             |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)               | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)若要获取此对象上**Irp-&gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)若要获取此对象上[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;MdlAddress**)。 |
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | 为生成内存描述符列表 (MDL) **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)若要获取此对象上**Irp-&gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)若要获取此对象上[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;MdlAddress**)。 |

 

 

 





