---
title: OPLOCK\_键\_ECP\_上下文结构
description: OPLOCK\_密钥\_ECP\_上下文结构用于将 oplock 密钥附加到文件中。
ms.assetid: 029dd105-162a-4674-a3d5-b54a91fa4be2
keywords:
- OPLOCK_KEY_ECP_CONTEXT 结构可安装的文件系统驱动程序
- POPLOCK_KEY_ECP_CONTEXT 结构指针可安装的文件系统驱动程序
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
ms.openlocfilehash: ad9d4dc68f3dadaf050230560cda08bea52d60b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841047"
---
# <a name="oplock_key_ecp_context-structure"></a>OPLOCK\_键\_ECP\_上下文结构


OPLOCK\_密钥\_ECP\_上下文结构用于将 oplock 密钥附加到文件中。

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
Oplock 项的 GUID。 此 GUID 在不同的句柄之间共享，并将其标识为属于相同的客户端缓存。 当两个句柄共享同一个 oplock 键时，在一个句柄上执行的请求将不会中断另一个句柄上的未完成 oplock。

**保护**  
保留。 必须设置为零。

<a name="remarks"></a>备注
-------

有关如何使用 ECPs 在创建文件时将附加信息与文件相关联的信息，请参阅将[额外的 Create 参数与 IRP\_MJ 一起使用\_创建操作](https://docs.microsoft.com/windows-hardware/drivers/ifs/using-extra-create-parameters-with-an-irp-mj-create-operation)。

OPLOCK\_键\_ECP\_上下文结构为只读。 你应使用它来仅检索有关 oplock 密钥 ECP 的信息。 有关此问题的详细信息，请参阅[系统定义的 ECPs](https://docs.microsoft.com/windows-hardware/drivers/ifs/system-defined-ecps)。

使用 oplock 键，应用程序可以在不中断应用程序自身 oplock 的情况下，在同一流中打开多个句柄。 Oplock 中断仅发生在应用程序收到共享冲突（状态\_共享\_冲突）之后。

打开流时，将在流句柄上授予 oplock。 此类流句柄可以与 oplock 键关联。 调用方可以向[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)例程显式提供 oplock 密钥，以创建流句柄。 如果调用方在调用方创建句柄时未显式指定 oplock 键，则操作系统会将句柄视为具有与句柄关联的唯一 oplock 键，使句柄的键与任何其他句柄上的任何其他键不同。 如果在不是对其授予 oplock 的句柄上接收到文件操作，并且与 oplock 的句柄关联的 oplock 密钥不同于与操作的句柄关联的键，并且该操作与当前已授予 oplock，则会破坏 oplock。 即使 oplock 与执行不兼容操作的进程或线程相同，也会中断。 例如，如果某一进程打开一个流，其中将为其授予独占 oplock，并使用不同的（或不存在） oplock 键再次打开相同的流，则会立即中断独占操作锁定。

创建句柄时，Oplock 项与句柄关联。 即使未授予任何 oplock，你也可以将句柄与 oplock 项关联。

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
<td align="left"><p>版本</p></td>
<td align="left"><p>从 Windows 7 开始提供此结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs 或 Ntddk）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)

 

 






