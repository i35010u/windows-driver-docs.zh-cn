---
title: WDF 缓冲区指针的 WDM 等效项
description: WDF 缓冲区指针的 WDM 等效项
ms.assetid: 7923A3CA-479A-4C7D-B428-F57C9701906E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abb7431bfd12eab85ea1071b587fc94c019a1b0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566339"
---
# <a name="wdm-equivalents-for-wdf-buffer-pointers"></a>WDF 缓冲区指针的 WDM 等效项


内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序使用以下方法来检索用于缓冲和直接 I/O 的 I/O 缓冲区。 除非另行指定，方法适用于 KMDF 和 UMDF。

-   [**WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)
-   [**WdfRequestRetrieveOutputWdmMdl (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff550021)
-   [**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)
-   [**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)
-   [**WdfRequestRetrieveInputWdmMdl (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff550016)
-   [**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)

下表描述了 IRP 的检索方法返回什么\_MJ\_读取、 IRP\_MJ\_写入和 IRP\_MJ\_设备\_控件请求缓冲和直接 I/O。 既不 I/O 请求需要特殊处理，因为该驱动程序必须在请求的用户模式进程的上下文中运行时检索缓冲区。

## <a href="" id="read"></a>IRP 的缓冲区\_MJ\_读取的请求


若要检索的读取请求的缓冲区，KMDF 驱动程序调用其中一种 **WdfRequestRetrieveOutput * * * Xxx*方法。 缓冲区的每个这些方法返回各不相同，具体取决于驱动程序是否执行缓冲或直接 I/O。 下表描述了每个方法在 WDM 术语中返回的指针。

| 函数                                                                             | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff550021) | 为生成内存描述符列表 (MDL) **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)             | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)若要获取此对象上**Irp-&gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)若要获取此对象上[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp&gt;MdlAddress**)。 |

 

## <a href="" id="write"></a>IRP 的缓冲区\_MJ\_写入请求


若要检索的写入请求的缓冲区，KMDF 驱动程序调用其中一种 **WdfRequestRetrieveInput * * * Xxx*方法。 缓冲区的每个这些方法返回各不相同，具体取决于驱动程序是否执行缓冲或直接 I/O。 下表描述了每个方法在 WDM 术语中返回的指针。

| 函数                                                                           | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff550016) | 生成有关 MDL **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                                                   | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)             | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)若要获取此对象上**Irp-&gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)若要获取此对象上[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp&gt;MdlAddress**)。 |

 

## <a href="" id="device-control"></a>IRP 的缓冲区\_MJ\_设备\_控制请求


若要检索设备 I/O 控制请求的缓冲区，KMDF 驱动程序调用任一**WdfRequestRetrieveInputXxx**或**WdfRequestRetrieveOutputXxx**方法。 缓冲区的每个这些方法返回各不相同，具体取决于驱动程序的执行是否[缓冲或直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff540701)下, 表中所示：

| 函数                                                                             | 缓冲的 I/O                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)               | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff550016)   | 生成有关 MDL **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                                                   | 生成有关 MDL **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                                                                                                             |
| [**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)               | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)若要获取此对象上**Irp-&gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)若要获取此对象上[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp&gt;MdlAddress**)。 |
| [**WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff550021) | 为生成内存描述符列表 (MDL) **Irp-&gt;AssociatedIrp.SystemBuffer** ，并返回 MDL。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)             | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)若要获取此对象上**Irp-&gt;AssociatedIrp.SystemBuffer**。 | 返回 WDFMEMORY 对象。 调用[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)若要获取此对象上[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp&gt;MdlAddress**)。 |

 

 

 





