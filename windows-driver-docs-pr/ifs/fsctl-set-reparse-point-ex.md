---
title: FSCTL_SET_REPARSE_POINT_EX 控制代码
description: FSCTL_SET_REPARSE_POINT_EX 控制代码对文件或目录设置重新分析点。
keywords:
- FSCTL_SET_REPARSE_POINT_EX 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_REPARSE_POINT_EX
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: e69ebaea55df7e1cb67c31366da8cad51cedc2ce
ms.sourcegitcommit: 4a4af9735e55c3314a8dc8931cb6bd21653d481d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "96518149"
---
# <a name="fsctl_set_reparse_point_ex-control-code"></a>FSCTL_SET_REPARSE_POINT_EX 控制代码

FSCTL_SET_REPARSE_POINT_EX 控制代码对文件或目录设置重新分析点。

若要执行此操作，请调用具有以下参数的 [**ZwFsControlFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwfscontrolfile) 。

Minifilters 应使用 [**FltTagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile) 而不是 FSCTL_SET_REPARSE_POINT_EX 来设置重新分析点。

有关重新分析点和 FSCTL_SET_REPARSE_POINT_EX 控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

## <a name="parameters"></a>参数

*FileHandle*  
要设置重新分析点的文件或目录的文件句柄。 此参数是必需的，不能为 **NULL**。

*FsControlCode*  
操作的控制代码。 使用 FSCTL_SET_REPARSE_POINT_EX 执行此操作。

*InputBuffer*  
指向分配的调用方 [**REPARSE_GUID_DATA_BUFFER**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer) 或包含重新分析点数据 [**REPARSE_DATA_BUFFER_EX**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer_ex) 结构的指针。

*InputBufferLength*  
*InputBuffer* 参数指向的缓冲区的大小（以字节为单位）。 对于 REPARSE_GUID_DATA_BUFFER 结构，此值必须至少是 REPARSE_GUID_DATA_BUFFER_HEADER_SIZE，加上用户定义数据的大小，并且必须小于或等于 MAXIMUM_REPARSE_DATA_BUFFER_SIZE。 对于 REPARSE_DATA_BUFFER_EX 结构，此值必须至少是 REPARSE_DATA_BUFFER_HEADER_SIZE，加上用户定义数据的大小，并且必须小于或等于 MAXIMUM_REPARSE_DATA_BUFFER_SIZE。

*OutputBuffer*  
不与此操作一起使用;设置为 **NULL**。

*OutputBufferLength*  
不与此操作一起使用;设置为零。

## <a name="status-block"></a>状态块

[**ZwFsControlFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwfscontrolfile) 返回 STATUS_SUCCESS 或适当的 NTSTATUS 值，如下所示：

| 值 | 描述 |
| ----- | ----------- |
| STATUS_DIRECTORY_NOT_EMPTY | 不能对非空目录设置重新分析点。 这是一个错误代码。|
| STATUS_EAS_NOT_SUPPORTED | 如果此请求在事务中，则无法对文件设置重新分析点。 这是一个错误代码。|
 | STATUS_IO_REPARSE_DATA_INVALID | 指定的参数值之一无效。 这是一个错误代码。|
| STATUS_IO_REPARSE_TAG_MISMATCH | 调用方指定的重新分析标记与要修改的重新分析点的标记不匹配。 这是一个错误代码。|
 | STATUS_NOT_A_REPARSE_POINT | 文件或目录不是重新分析点。 这是一个错误代码。|
| STATUS_REPARSE_ATTRIBUTE_CONFLICT | 重新分析点是第三方重新分析点，调用方指定的重新分析 GUID 与要修改的重新分析点的 GUID 不匹配。 这是一个错误代码。|

### <a name="requirements"></a>要求

* 标头： Ntifs (包含 Ntifs 或 Fltkernel) 

## <a name="see-also"></a>另请参阅

[**IRP_MJ_FILE_SYSTEM_CONTROL 的 FLT_PARAMETERS**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltTagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL_DELETE_REPARSE_POINT**](fsctl-delete-reparse-point.md)

[**FSCTL_GET_REPARSE_POINT**](fsctl-get-reparse-point.md)

[**IRP_MJ_FILE_SYSTEM_CONTROL**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**REPARSE_DATA_BUFFER_EX**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer_ex)

[**REPARSE_GUID_DATA_BUFFER**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwfscontrolfile)
