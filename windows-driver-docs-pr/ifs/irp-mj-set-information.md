---
title: 'IRP_MJ_SET_INFORMATION (IFS) '
description: IRP_MJ_SET_INFORMATION
keywords:
- IRP_MJ_SET_INFORMATION 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_SET_INFORMATION
api_type:
- NA
ms.date: 01/14/2021
ms.localizationpriority: medium
ms.openlocfilehash: 42d8c08b945454b7e59de8c31189b6885efb8bd5
ms.sourcegitcommit: 5feac22fc1a86b799fab3aa939adfa1df92f53a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2021
ms.locfileid: "98533987"
---
# <a name="irp_mj_set_information-ifs"></a>IRP_MJ_SET_INFORMATION (IFS) 

## <a name="when-sent"></a>发送时间

IRP_MJ_SET_INFORMATION 请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，可以在用户模式应用程序调用 Microsoft Win32 函数（如 **SetEndOfFile** ）或内核模式组件调用 [**ZwSetInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)时发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序

文件系统驱动程序应提取并解码文件对象，以确定它是表示用户文件还是打开目录。 如果是这样，则文件系统驱动程序应适当处理请求并完成 IRP。

可以在文件 *和* 目录上设置以下类型的信息：

* FileBasicInformation
* FileDispositionInformation
* 允许在目录层次结构中创建循环的文件系统的 FileLinkInformation () 
* FilePositionInformation
* FileRenameInformation

只能对文件设置以下类型的信息：

* FileAllocationInformation
* FileEndOfFileInformation
* FileLinkInformation (用于不允许在目录层次结构中创建循环的文件系统（例如 NTFS）) 
* FileValidDataLengthInformation

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序

筛选器驱动程序必须将此 IRP 传递到堆栈上的下一个较低版本的驱动程序。

## <a name="parameters"></a>参数

文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理 set file information 请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

*DeviceObject*：指向目标设备对象的指针。

*Irp->AssociatedIrp.SystemBuffer*：指向包含要设置的文件或目录信息的输入缓冲区的指针。 此信息存储在以下结构之一中：

* [**FILE_ALLOCATION_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)
* [**FILE_BASIC_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)
* [**FILE_DISPOSITION_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)
* [**FILE_END_OF_FILE_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)
* [**FILE_LINK_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)
* [**FILE_POSITION_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)
* [**FILE_RENAME_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)
* [**FILE_VALID_DATA_LENGTH_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)

*Irp->IoStatus*：指向 [**IO_STATUS_BLOCK**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。 有关详细信息，请参阅 [**ZwSetInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)的 *IoStatusBlock* 参数说明。

*IrpSp->FileObject*：指向与 *DeviceObject* 关联的文件对象的指针。 此参数包含指向 **RelatedFileObject** 字段的指针，该字段也是 FILE_OBJECT 结构。 FILE_OBJECT 结构的 **RelatedFileObject** 字段在处理 IRP_MJ_SET_INFORMATION 期间无效，不应使用。

*IrpSp->MajorFunction*：设置为 IRP_MJ_SET_INFORMATION。

*IrpSp->MinorFunction*：当 *IRP >SetFile FileInformationClass* 为 **FileValidDataLengthInformation** 时，可以 IRP_MN_KERNEL_CALL。 这表明请求的源是受信任的内核组件，允许驱动程序绕过安全检查。

*IrpSp->SetFile. AdvanceOnly*： file 结尾操作的标志。 这会确定在 **FileInformationClass** FileEndOfFileInformation 时， [**FILE_END_OF_FILE_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)结构使用 **EndOfFile** 成员  ==  。 如果 **为 TRUE**，则仅当文件增加当前有效数据长度时，才从 **EndOfFile** 设置新的有效数据长度。 如果 **为 FALSE**，则从 **EndOfFile** 设置新的文件大小。

*IrpSp->SetFile. ClusterCount*：保留供系统使用。

*IrpSp->SetFile. DeleteHandle*：保留供系统使用。

*IrpSp->SetFile. FileInformationClass*：要为文件设置的信息类型。 下列类型作之一：

| 值 | 含义 |
| ----- | ------- |
| **FileAllocationInformation** | 为文件设置 [**FILE_ALLOCATION_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information) 。 |
| **FileBasicInformation** | 为文件设置 [**FILE_BASIC_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information) 。 |
| **FileDispositionInformation** | 为文件设置 [**FILE_DISPOSITION_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information) 。 |
| **FileEndOfFileInformation** | 为文件设置 [**FILE_END_OF_FILE_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information) 。 |
| **FileLinkInformation** | 为文件设置 [**FILE_LINK_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information) 。 |
| **FilePositionInformation** | 为文件设置 [**FILE_POSITION_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information) 。 |
| **FileRenameInformation** | 为文件设置 [**FILE_RENAME_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information) 。 |
| **FileValidDataLengthInformation** | 为文件设置 [**FILE_VALID_DATA_LENGTH_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information) 。 有关其他信息，请参阅 *Irp->MinorFunction* 。 |

*IrpSp->SetFile*：用于重命名或链接操作。 如果 *irp >AssociatedIrp.SystemBuffer->FileName* 包含完全限定的文件名，或者如果 *Irp->AssociatedIrp.SysTemBuffer->RootDirectory* 为非 **NULL**，则此成员是作为操作目标的文件的父目录的文件对象指针。 否则为 **NULL**。

*IrpSp >-* *>AssociatedIrp.SystemBuffer* 所指向的缓冲区的长度（以字节为单位）。

*IrpSp->ReplaceIfExists*：设置为 **TRUE** 以指定如果已存在同名的文件，则应将其替换为给定的文件。 如果重命名操作在已存在具有给定名称的文件时失败，则设置为 **FALSE** 。

## <a name="remarks"></a>注解

缓存管理器将 **AdvanceOnly** 成员设置为 **TRUE** ，以通知文件系统将磁盘上的当前有效数据长度提升到 **EndOfFile** 中的新有效数据长度。 如果 **AdvanceOnly** 为 **FALSE**，则会设置 **EndOfFile** 成员中的新文件大小，该大小可大于或小于当前文件大小。

## <a name="see-also"></a>另请参阅

[**FILE_ALLOCATION_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)

[**FILE_BASIC_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**FILE_DISPOSITION_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)

[**FILE_END_OF_FILE_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)

[**FILE_LINK_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)

[**FILE_POSITION_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**FILE_RENAME_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)

[**FILE_VALID_DATA_LENGTH_INFORMATION**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)

[**IO_STACK_LOCATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO_STATUS_BLOCK**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP_MJ_QUERY_INFORMATION**](irp-mj-query-information.md)

[**ZwSetInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)
