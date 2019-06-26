---
title: OPLOCK\_键\_ECP\_上下文结构
description: OPLOCK\_键\_ECP\_上下文结构用于将 oplock 密钥附加到文件。
ms.assetid: 029dd105-162a-4674-a3d5-b54a91fa4be2
keywords:
- OPLOCK_KEY_ECP_CONTEXT 结构可安装文件系统驱动程序
- POPLOCK_KEY_ECP_CONTEXT 结构指针可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- OPLOCK_KEY_ECP_CONTEXT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66e9a5a51f8e9688822d47f04e14195da4533a81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386068"
---
# <a name="oplockkeyecpcontext-structure"></a>OPLOCK\_键\_ECP\_上下文结构


OPLOCK\_键\_ECP\_上下文结构用于将 oplock 密钥附加到文件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _OPLOCK_KEY_ECP_CONTEXT {
  GUID  OplockKey;
  ULONG Reserved;
} OPLOCK_KEY_ECP_CONTEXT, *POPLOCK_KEY_ECP_CONTEXT;
```

<a name="members"></a>成员
-------

**OplockKey**  
Oplock 密钥的 GUID。 此 GUID 在不同的图柄之间共享，并将它们标识为属于相同的客户端缓存。 当两个句柄共享相同的 oplock 键时上一个句柄, 执行的请求不会对其他句柄中断未完成的机会锁。

**保留**  
保留。 必须设置为零。

<a name="remarks"></a>备注
-------

若要了解如何使用 ECPs 时创建的文件使用文件关联的额外信息，请参阅[使用额外创建的参数与 IRP\_MJ\_创建操作](https://docs.microsoft.com/windows-hardware/drivers/ifs/using-extra-create-parameters-with-an-irp-mj-create-operation)。

OPLOCK\_键\_ECP\_上下文结构是只读的。 应使用它来检索有关 oplock ECP 仅密钥信息。 有关此问题的详细信息，请参阅[系统定义 ECPs](https://docs.microsoft.com/windows-hardware/drivers/ifs/system-defined-ecps)。

Oplock 密钥启用应用程序以打开到同一个流的多个句柄而不会中断应用程序自身 oplock。 需要破坏 oplock 仅发生后，应用程序收到了共享冲突 (状态\_共享\_冲突)。

流句柄被授予 Oplock 时打开的流。 此类的流句柄可以与 oplock 键相关联。 调用方可以显式提供的 oplock 关键[ **IoCreateFileEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)例程，以创建流句柄。 如果调用方未显式指定 oplock 键时调用方创建句柄，操作系统会为具有与句柄，关联的唯一机会锁密钥，以便该句柄的密钥不同于其他任何句柄上的任何其他键将句柄。 如果对已授予 oplock，以外的句柄上收到的文件操作和与 oplock 句柄关联的 oplock 密钥不同于与操作的句柄关联的密钥和该操作与不兼容当前授予 oplock，然后该 oplock 已断开。 即使是相同的进程或线程执行不兼容的操作会中断 oplock。 例如，如果一个进程打开的流为其授予独占 oplock，并且在同一进程然后同一个流将再次打开，通过使用不同 （或无） oplock 密钥，排他 oplock 被窃立即。

创建句柄时，Oplock 密钥是与句柄相关联。 即使在不授予任何 oplock，可以使用 oplock 密钥将句柄相关联。

有关 oplock 和 oplock 密钥的详细信息，请参阅[Oplock 语义概述](https://docs.microsoft.com/windows-hardware/drivers/ifs/overview)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>此结构是从 Windows 7 开始提供。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Ntddk.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)

 

 






