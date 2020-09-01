---
title: 双重 \_ OPLOCK \_ 关键 \_ ECP \_ 上下文结构
description: 双重 \_ oplock \_ 键 \_ ECP \_ 上下文结构包含双重 oplock 键的额外 create 参数上下文。 可在此结构中设置目标和父文件对象的 oplock 键。
ms.assetid: 7E337D2F-7292-4D18-B750-8361A83C8B1F
keywords:
- DUAL_OPLOCK_KEY_ECP_CONTEXT 结构可安装文件系统驱动程序
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
ms.openlocfilehash: 00d247f838e4767c2c17ce00b2cb60a441deab32
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065306"
---
# <a name="dual_oplock_key_ecp_context-structure"></a>双重 \_ OPLOCK \_ 关键 \_ ECP \_ 上下文结构


**双重 \_ oplock \_ 键 \_ ECP \_ 上下文**结构包含双重 oplock 键的额外 create 参数上下文。 可在此结构中设置目标和父文件对象的 oplock 键。

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
表示父 oplock 项值的 **GUID** 。

**TargetOplockKey**  
表示目标 oplock 项值的 **GUID** 。

**ParentOplockKeySet**  
如果 **ParentOplockKey** 包含父的 oplock 密钥的有效 GUID，则设置为 TRUE。

**TargetOplockKeySet**  
如果 **TargetOplockKey** 包含目标的 oplock 密钥的有效 GUID，则设置为 TRUE。

<a name="remarks"></a>备注
-------

**双重 \_ oplock \_ 键 \_ ECP \_ 上下文**结构提供双 oplock 键，以允许对文件和目录的请求进行 OPLOCK。 与[**OPLOCK \_ key \_ ecp \_ 上下文**](oplock-key-ecp-context.md)结构一样，在创建由文件系统或文件系统筛选器驱动程序[** \_ \_ 创建的 IRP MJ**](irp-mj-create.md)时，将在额外的 create parameter list ([**ECP \_ list**](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))) 及更高版本中设置与文件对象关联的额外 create 参数列表中设置了**双重 \_ oplock \_ 密钥 \_ ecp \_ 上下文**。

在调用[**FsRtlAllocateExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameter)、 [**FsRtlInitializeExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitializeextracreateparameter)或[**FltRemoveExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltremoveextracreateparameter)等支持例程时，将使用值**GUID \_ ECP \_ 双重 \_ OPLOCK \_ 键**。

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
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ECP \_ 列表**](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))

[**IO \_ 驱动程序 \_ 创建 \_ 上下文**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)

[**IoCreateFileEx**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)

[**IRP \_ MJ \_ 创建**](irp-mj-create.md)

[**OPLOCK \_ 密钥 \_ ECP \_ 上下文**](oplock-key-ecp-context.md)


 

