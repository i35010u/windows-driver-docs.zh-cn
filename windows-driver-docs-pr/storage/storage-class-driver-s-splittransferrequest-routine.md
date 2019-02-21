---
title: 存储类驱动程序 SplitTransferRequest 例程
description: 存储类驱动程序 SplitTransferRequest 例程
ms.assetid: 4f449d3b-9a0a-4ff9-a7fb-bfa21b8a56c0
keywords:
- SplitTransferRequest
- 非连续页 WDK 存储
- 拆分传输请求
- 转移请求拆分 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bfe1b3a3c36c55b8119b0e0a841454c8f96496c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521810"
---
# <a name="storage-class-drivers-splittransferrequest-routine"></a>存储类驱动程序 SplitTransferRequest 例程


## <span id="ddk_storage_class_drivers_splittransferrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SPLITTRANSFERREQUEST_ROUTINE_KG"></span>


存储\_适配器\_描述符数据返回给*GetDescriptor*例程指示类驱动程序到给定 HBA 的传输功能。 具体而言，此数据指示**MaximumTransferLength**以字节为单位， **MaximumPhysicalPages**： 即，多少个不连续页面 HBA 可以管理中的备份系统的物理内存缓冲区 （即，其分散/集中支持的范围）。

大多数类驱动程序存储到此配置数据的指针设备扩展的每个设备对象中，因为存储类驱动程序负责将拆分超出 HBA 的功能将数据传输的所有传输请求。 换而言之，类驱动程序的[ **DispatchReadWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程必须确定每个 IRP 是否请求多于 HBA 可以处理单个传输操作中的传输。

例如，此类*DispatchReadWrite*例程可以类似于以下代码：

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

在类驱动程序无法判断多少物理分隔线缓冲区将具有后映射，因此它必须假定在传输中的每一页是不连续和比较针对允许的物理分隔线数的页数。

请注意，此类的驱动程序的*DispatchReadWrite*例程调用**IoMarkIrpPending** ，并返回状态\_PENDING 后立即调用其*SplitTransferRequest*例程替换原始 IRP。

若要执行原始传输请求，驱动程序的*SplitTransferRequest*例程创建了一个或多个 Irp，以处理 subbuffers 大小将调整为适应 HBA 的功能。 对于每个此类 IRP *SplitTransferRequest*例程：

-   通过调用内部通常设置 SRB *BuildRequest*例程 (请参阅[存储类驱动程序 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md))

-   副本 MDL 从原始 IRP 地址到新的 IRP

-   集**DataBuffer**中为此传输的一段 MDL 字节中的偏移量 SRB

-   设置其*IoCompletion*例程之前发送到端口驱动程序和 IRP [ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

若要跟踪的传输，每个部分*SplitTransferRequest*注册*IoCompletion*向较低的下一步驱动程序发送的每个驱动程序分配的 IRP 例程。 *IoCompletion*例程维护原始 IRP 中的已完成的部分传输请求的计数使用**InterlockedIncrement**并**InterlockedDecrement**到请确保计数准确。

此类*IoCompletion*例程必须释放任何 Irp 和/或 Srb 驱动程序已分配，但必须完成原始 IRP，或者在类驱动程序已经用完了 IRP 的重试和必须故障时转移所有请求的数据它由于设备传输错误。

 

 




