---
title: 存储类驱动程序的 SplitTransferRequest 例程
description: 存储类驱动程序的 SplitTransferRequest 例程
ms.assetid: 4f449d3b-9a0a-4ff9-a7fb-bfa21b8a56c0
keywords:
- SplitTransferRequest
- 不连续的页面 WDK 存储
- 拆分传输请求
- 传输请求拆分 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3420d968d87a9822cb1c8bd377a17f839e80d81d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841607"
---
# <a name="storage-class-drivers-splittransferrequest-routine"></a>存储类驱动程序的 SplitTransferRequest 例程


## <span id="ddk_storage_class_drivers_splittransferrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SPLITTRANSFERREQUEST_ROUTINE_KG"></span>


返回到*GetDescriptor*例程的存储\_适配器\_描述符数据指示给定 HBA 到类驱动程序的传输功能。 具体而言，此数据指示**MaximumTransferLength** （以字节为单位）和**MaximumPhysicalPages**：也就是说，HBA 可以在支持系统缓冲区的物理内存（即，其散播/收集支持）。

大多数类驱动程序在每个设备对象的设备扩展中存储指向此配置数据的指针，因为存储类驱动程序负责拆分超过 HBA 传输数据的所有传输请求。 换句话说，类驱动程序的[**DispatchReadWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程必须确定每个 IRP 是否请求的传输超过 HBA 可以在单个传输操作中处理的情况。

例如，此类*DispatchReadWrite*例程可能包含类似于下面的代码：

```cpp
PSTORAGE_ADAPTER_DESCRIPTOR adapterDescriptor = 
    commonExtension->PartitionZeroExtension->AdapterDescriptor;
ULONG transferPages;
ULONG maximumTransferLength = 
    adapterDescriptor->MaximumTransferLength;
    :        : 
// 
// Calculate number of pages in this transfer 
// 
transferPages = ADDRESS_AND_SIZE_TO_SPAN_PAGES( 
                    MmGetMdlVirtualAddress(Irp->MdlAddress), 
                        currentIrpStack->Parameters.Read.Length);
// 
// Check whether requested length is greater than the maximum number 
// of bytes that can be transferred in a single operation 
// 
if (currentIrpStack->Parameters.Read.Length > maximumTransferLength ||
        transferPages > adapterDescriptor->MaximumPhysicalPages) { 
    transferPages = adapterDescriptor->MaximumPhysicalPages - 1;
    if (maximumTransferLength > transferPages << PAGE_SHIFT) { 
        maximumTransferLength = transferPages << PAGE_SHIFT; 
    } 
    IoMarkIrpPending(Irp); 
    SplitTransferRequest(DeviceObject, 
                            Irp, 
                            maximumTransferLength); 
    return STATUS_PENDING; 
} 
    :        : 
```

类驱动程序无法判断缓冲区在被映射后将包含多少物理中断，因此它必须假定传输中的每一页都是不连续的，并根据允许的物理中断数来比较页的数目。

请注意，在使用原始 IRP 调用其*SplitTransferRequest*例程后，此类驱动程序的*DispatchReadWrite*例程将调用**也**并返回状态\_立即挂起。

若要执行原始传输请求，驱动程序的*SplitTransferRequest*例程会创建一个或多个 irp 来处理调整大小以适合 HBA 功能的 subbuffers。 对于每个此类 IRP， *SplitTransferRequest*例程：

-   通常通过调用内部*BuildRequest*例程来设置 SRB （请参阅[存储类驱动程序的 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)）

-   将 MDL 地址从原始 IRP 复制到新 IRP

-   将 SRB 中的**DataBuffer**设置为这部分传输的 MDL 中的偏移量（以字节为单位）

-   在将 IRP 发送到带有[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的端口驱动程序之前设置其*IoCompletion*例程

为了跟踪传输的每个部分， *SplitTransferRequest*会为它发送到下一个较低驱动程序的每个由驱动程序分配的 IRP 注册一个*IoCompletion*例程。 *IoCompletion*例程使用**InterlockedIncrement**和**InterlockedDecrement**来维护原始 IRP 中已完成的部分传输请求计数，以确保计数准确无误。

此类*IoCompletion*例程必须释放已分配的任何 irp 和/或 SRBs，并在传输所有请求的数据或类驱动程序已用尽 irp 的重试时完成原始 IRP，并必须在设备传输错误。

 

 




