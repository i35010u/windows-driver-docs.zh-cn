---
title: IRP_MJ_QUERY_QUOTA
description: IRP \_ MJ \_ 查询 \_ 配额
ms.assetid: eb48b5ef-7eac-49d4-ab23-2d3efe783fa3
keywords:
- IRP_MJ_QUERY_QUOTA 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_QUOTA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d765ae4f22c4fe2d5a8f46679211cd68c6f9d98
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063064"
---
# <a name="irp_mj_query_quota"></a>IRP \_ MJ \_ 查询 \_ 配额

## <a name="when-sent"></a>发送时间

IRP \_ MJ \_ 查询 \_ 配额请求由 i/o 管理器发送。 例如，在用户模式应用程序调用了 Microsoft Win32 方法（如 **IDiskQuotaControl：： GetQuotaState**）时，可以发送此请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序

如果文件系统支持磁盘配额，则文件系统驱动程序应提取并解码文件对象，以确定它是否表示用户打开了文件或目录。 如果是这样，则驱动程序应处理查询并完成 IRP。 否则，驱动程序应视需要完成 IRP，而不处理查询。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序

筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序，除非它需要显式覆盖配额行为。

## <a name="parameters"></a>parameters

文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理查询配额信息请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

### <a name="deviceobject"></a>*DeviceObject*  

指向目标设备对象的指针。

### <a name="deviceobject-flags"></a>*DeviceObject->标志*  

按 \_ 如下所示使用 "执行缓冲 IO" 和 " \_ 执行 \_ 直接 IO" \_ 标志来指定将数据传递给驱动程序的方法：

|标志设置|I/o 方法|
|----|----|
|~ DO_BUFFERED_IO|~ DO_DIRECT_IO|
|METHOD_NEITHER|~ DO_BUFFERED_IO|
|DO_DIRECT_IO|METHOD_DIRECT|
|DO_BUFFERED_IO|~ DO_DIRECT_IO|
|METHOD_BUFFERED|DO_BUFFERED_IO|
|DO_DIRECT_IO|METHOD_BUFFERED|

### <a name="irp-associatedirpsystembuffer"></a>*Irp->AssociatedIrp.SystemBuffer*

一个指针，指向系统提供的用于中间系统缓冲区的缓冲区（如果 \_ \_ 在 *DeviceObject->标志*中设置了 "执行缓冲 IO" 标记）。 否则，此成员设置为 **NULL**。

### <a name="irp-iostatus"></a>*Irp->IoStatus*

指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

### <a name="irp-userbuffer"></a>*Irp->UserBuffer*  

一个指针，指向由调用方提供的文件 \_ 配额 \_ 信息结构化的输出缓冲区，该缓冲区用于接收卷的配额信息。

### <a name="irpsp-fileobject"></a>*IrpSp->FileObject*

指向与 *DeviceObject*关联的文件对象的指针。

*>IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 查询配额期间无效 \_ \_ ，不应使用。

### <a name="irpsp-flags"></a>*IrpSp->标志*

此成员可以是以下一项或多项：

|Flag|含义|
|----|----|
|SL_INDEX_SPECIFIED|从配额列表中的条目开始扫描，该配额列表中的索引由 *>IrpSp 指定。 QueryQuota. StartSid*|
|SL_RESTART_SCAN|从列表中的第一个条目开始扫描。 如果未设置此标志，则从上一个 IRP_MJ_QUERY_QUOTA 请求恢复扫描。|
|SL_RETURN_SINGLE_ENTRY|仅返回找到的第一个条目。|

### <a name="irpsp-majorfunction"></a>*IrpSp->MajorFunction*

指定 IRP \_ MJ \_ 查询 \_ 配额。

### <a name="irpsp-parametersqueryquotalength"></a>*IrpSp->参数. QueryQuota. 长度*

Irp 所指向的缓冲区的长度（以字节为单位） *>UserBuffer*。

### <a name="irpsp-parametersqueryquotasidlist"></a>*IrpSp->参数. QueryQuota. SidList*

指向要返回其配额信息的 Sid 列表的可选指针。 列表中的每个条目都是一个 [**文件 \_ 获取 \_ 配额 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_quota_information) 结构。 此结构的定义如下：

```cpp
typedef struct _FILE_GET_QUOTA_INFORMATION {
    ULONG NextEntryOffset;
    ULONG SidLength;
    SID Sid;
} FILE_GET_QUOTA_INFORMATION, *PFILE_GET_QUOTA_INFORMATION;
```

|成员|含义|
|-----|----|
|NextEntryOffset|下一个 FILE_GET_QUOTA_INFORMATION 条目的字节偏移量（如果缓冲区中存在多个条目）。 如果此成员不在此成员后面，则为零。|
|SidLength|**Sid**成员的长度（以字节为单位）。|
|Sid|SID)  (安全标识符|

### <a name="irpsp-parametersqueryquotasidlistlength"></a>*IrpSp->参数. QueryQuota. SidListLength*

Sid 列表的长度（以字节为单位）（如果已指定）。

#### <a name="irpsp-parametersqueryquotastartsid"></a>*IrpSp->参数. QueryQuota. StartSid*

指向某个 SID 的可选指针，它指示返回的信息是从第一个项之外的项开始。 如果指定 SID 列表，则忽略此参数。

## <a name="see-also"></a>另请参阅

[**FILE \_ 获取 \_ 配额 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_quota_information)

[**文件 \_ 配额 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckQuotaBufferValidity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 设置 \_ 配额**](irp-mj-set-quota.md)