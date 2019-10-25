---
title: 双\_OPLOCK\_键\_ECP\_上下文结构
description: 双\_OPLOCK\_键\_ECP\_上下文结构包含双重 oplock 键的额外 create 参数上下文。 可在此结构中设置目标和父文件对象的 oplock 键。
ms.assetid: 7E337D2F-7292-4D18-B750-8361A83C8B1F
keywords:
- DUAL_OPLOCK_KEY_ECP_CONTEXT 结构可安装的文件系统驱动程序
- PDUAL_OPLOCK_KEY_ECP_CONTEXT 结构指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- DUAL_OPLOCK_KEY_ECP_CONTEXT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6072e03f3ca9a44447bcd7cffd2ac7198ef2601
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841429"
---
# <a name="dual_oplock_key_ecp_context-structure"></a>双\_OPLOCK\_键\_ECP\_上下文结构


**双\_OPLOCK\_键\_ECP\_上下文**结构包含双重 oplock 键的额外 create 参数上下文。 可在此结构中设置目标和父文件对象的 oplock 键。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DUAL_OPLOCK_KEY_ECP_CONTEXT {
  GUID    ParentOplockKey;
  GUID    TargetOplockKey;
  BOOLEAN ParentOplockKeySet;
  BOOLEAN TargetOplockKeySet;
} DUAL_OPLOCK_KEY_ECP_CONTEXT, *PDUAL_OPLOCK_KEY_ECP_CONTEXT;
```

<a name="members"></a>成员
-------

**ParentOplockKey**  
表示父 oplock 项值的**GUID** 。

**TargetOplockKey**  
表示目标 oplock 项值的**GUID** 。

**ParentOplockKeySet**  
如果**ParentOplockKey**包含父的 oplock 密钥的有效 GUID，则设置为 TRUE。

**TargetOplockKeySet**  
如果**TargetOplockKey**包含目标的 oplock 密钥的有效 GUID，则设置为 TRUE。

<a name="remarks"></a>备注
-------

**双\_oplock\_键\_ECP\_上下文**结构提供双 oplock 键，以允许对文件和目录的请求进行 oplock。 类似于[**OPLOCK\_键\_ECP\_上下文**](oplock-key-ecp-context.md)结构、**双重\_OPLOCK\_键\_** 在额外的创建参数列表（[**ECP\_列表**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))）中设置，稍后与处理[**IRP\_MJ**](irp-mj-create.md)过程中的文件对象\_由文件系统或文件系统筛选器驱动程序创建。

调用支持例程（如[**FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)、 [**FsRtlInitializeExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546113)） [**时，使用值 GUID\_ECP\_双\_OPLOCK\_密钥FltRemoveExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltremoveextracreateparameter)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>此结构从 Windows 8 开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ECP\_列表**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))

[**IO\_驱动程序\_创建\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)

[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)

[**IRP\_MJ\_创建**](irp-mj-create.md)

[**OPLOCK\_键\_ECP\_上下文**](oplock-key-ecp-context.md)

[Oplock 语义](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-semantics)

 

 






