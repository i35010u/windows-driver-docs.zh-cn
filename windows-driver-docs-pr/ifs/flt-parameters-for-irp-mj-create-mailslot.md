---
title: IRP_MJ_CREATE_MAILSLOT 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_CREATE_MAILSLOT 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时，将使用以下联合组件。
ms.assetid: aa223d51-7d13-4244-bad5-db14f1fb0d2c
keywords:
- IRP_MJ_CREATE_MAILSLOT 联合文件系统驱动程序的 FLT_PARAMETERS
- FLT_PARAMETERS 联合文件系统驱动程序
- PFLT_PARAMETERS 联合指针文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: b46ebe0b1cd8e1ac448b7bfe48d6decc3d9a87a3
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065968"
---
# <a name="flt_parameters-for-irp_mj_create_mailslot-union"></a>IRP_MJ_CREATE_MAILSLOT 联合的 FLT_PARAMETERS

当[FLT_IO_PARAMETER_BLOCK](/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段[IRP_MJ_CREATE_MAILSLOT](irp-mj-create-mailslot.md)时，将使用[FLT_PARAMETERS](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)联合中的以下结构。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIO_SECURITY_CONTEXT     SecurityContext;
    ULONG                    Options;
    USHORT POINTER_ALIGNMENT Reserved;
    USHORT                   ShareAccess;
    PVOID                    Parameters;
  } CreateMailslot;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>成员

FLT_PARAMETERS 的 **CreateMailslot** 结构包含以下成员。

**SecurityContext**  
一个指向 [IO_SECURITY_CONTEXT](/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_security_context) 结构的指针，该结构表示 IRP_MJ_CREATE_MAILSLOT 请求的安全上下文，其中：

- **SecurityContext->AccessState** 是一个指向 [ACCESS_STATE](/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state) 结构的指针，该结构包含对象的主题上下文、授予访问类型和剩余所需的访问类型。

- **SecurityContext->DesiredAccess** 是一个 [ACCESS_MASK](../kernel/access-mask.md) 结构，它指定为 mailslot 请求的访问权限。 有关详细信息，请参阅[**FltCreateMailslotFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatemailslotfile)的*DesiredAccess*参数。

**选项**  
标志的位掩码，用于指定创建或打开 mailslot 时要应用的选项，以及当 mailslot 已经存在时要执行的操作。 此成员的低24位对应于**FltCreateMailslotFile**的*CreateOptions*参数。 高8位对应于**FltCreateMailslotFile**的*CreateDisposition*参数。

**预留**  
保护请勿使用。

**ShareAccess**  
为 mailslot 文件请求的共享访问权限位掩码。 如果此参数为零，则请求独占访问。 有关详细信息，请参阅[**FltCreateMailslotFile**](/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatemailslotfile)的*ShareAccess*参数。

**参数**  
指向 [MAILSLOT_CREATE_PARAMETERS](/windows-hardware/drivers/ddi/wdm/ns-wdm-_mailslot_create_parameters) 结构的指针，该结构包含正在创建或打开的 MAILSLOT 的相关信息。


## <a name="remarks"></a>备注

IRP_MJ_CREATE_MAILSLOT i/o 操作时， [FLT_PARAMETERS](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)包含**CreateMailslot**结构。 I/o 操作由[FLT_CALLBACK_DATA](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)结构表示，操作参数包含在回调数据的*Iopb*参数指向的[FLT_IO_PARAMETER_BLOCK](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构内。

已注册 IRP_MJ_CREATE_MAILSLOT 操作的回调例程的文件系统微筛选器驱动程序应执行任何所需的处理和返回操作。

请注意，除最后一个 longword 字段外， **CreateMailslot** 结构中的字段必须与 **Create** 结构的字段相匹配。

IRP_MJ_CREATE_MAILSLOT 是基于 IRP 的操作。

## <a name="requirements"></a>要求

**标头**： Fltkernel (包含 Fltkernel) 


## <a name="see-also"></a>另请参阅

[ACCESS_MASK](../kernel/access-mask.md)

[ACCESS_STATE](/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)

[FLT_CALLBACK_DATA](/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[FLT_PARAMETERS](/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateMailslotFile**](/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatemailslotfile)

[IRP_MJ_CREATE_MAILSLOT](irp-mj-create-mailslot.md)

[MAILSLOT_CREATE_PARAMETERS](/windows-hardware/drivers/ddi/wdm/ns-wdm-_mailslot_create_parameters)