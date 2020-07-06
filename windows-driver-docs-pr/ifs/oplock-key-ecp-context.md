---
title: OPLOCK_KEY_ECP_CONTEXT 结构
description: OPLOCK_KEY_ECP_CONTEXT 结构用于将 OPLOCK 密钥附加到文件中。
ms.assetid: 029dd105-162a-4674-a3d5-b54a91fa4be2
keywords:
- OPLOCK_KEY_ECP_CONTEXT 结构可安装文件系统驱动程序
- POPLOCK_KEY_ECP_CONTEXT 结构指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- OPLOCK_KEY_ECP_CONTEXT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 898b5ffdedaf01a43c33317ceee7d38aa7120115
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967958"
---
# <a name="oplock_key_ecp_context-structure"></a>OPLOCK_KEY_ECP_CONTEXT 结构

OPLOCK_KEY_ECP_CONTEXT 结构用于将 OPLOCK 密钥附加到文件中。 此结构在 Windows 8 及更高版本中已过时;筛选器应改为使用[DUAL_OP_LOCK_KEY_ECP_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ifs/dual-oplock-key-ecp-context)。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef struct _OPLOCK_KEY_ECP_CONTEXT {
  GUID  OplockKey;
  ULONG Reserved;
} OPLOCK_KEY_ECP_CONTEXT, *POPLOCK_KEY_ECP_CONTEXT;
```

## <a name="members"></a>成员

**OplockKey**  
Oplock 项的 GUID。 此 GUID 在不同的句柄之间共享，并将其标识为属于相同的客户端缓存。 当两个句柄共享同一个 oplock 键时，在一个句柄上执行的请求将不会中断另一个句柄上的未完成 oplock。

**保留**  
保留。 必须设置为零。

## <a name="remarks"></a>备注

有关如何使用 ECPs 在创建文件时将附加信息与文件相关联的信息，请参阅将[额外的 Create 参数与 IRP_MJ_CREATE 操作一起使用](https://docs.microsoft.com/windows-hardware/drivers/ifs/using-extra-create-parameters-with-an-irp-mj-create-operation)。

如果微筛选器看到上方的 ECP，则不应更改 OPLOCK_KEY_ECP_CONTEXT 结构的内容。 你应使用它来仅检索有关 oplock 密钥 ECP 的信息。 有关此问题的详细信息，请参阅[系统定义的 ECPs](https://docs.microsoft.com/windows-hardware/drivers/ifs/system-defined-ecps)。

使用 oplock 键，应用程序可以在不中断应用程序自身 oplock 的情况下，在同一流中打开多个句柄。 Oplock 中断仅在应用程序收到共享冲突（STATUS_SHARING_VIOLATION）后发生。

打开流时，将在流句柄上授予 oplock。 此类流句柄可以与 oplock 键关联。 调用方可以向[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)例程显式提供 oplock 密钥，以创建流句柄。 如果调用方在调用方创建句柄时未显式指定 oplock 键，则操作系统会将句柄视为具有与句柄关联的唯一 oplock 键，使句柄的键与任何其他句柄上的任何其他键不同。 如果在不是被授权者的句柄上接收到文件操作，并且与 oplock 的句柄关联的 oplock 密钥不同于与操作的句柄关联的键，并且该操作与当前授予的 oplock 不兼容，则该 oplock 会断开。 即使 oplock 与执行不兼容操作的进程或线程相同，也会中断。 例如，如果某一进程打开一个流，其中将为其授予独占 oplock，并使用不同的（或不存在） oplock 键再次打开相同的流，则会立即中断独占操作锁定。

创建句柄时，Oplock 项与句柄关联。 即使未授予任何 oplock，你也可以将句柄与 oplock 项关联。

有关 oplock 和 oplock 密钥的详细信息，请参阅[Oplock 语义概述](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-overview)。

## <a name="requirements"></a>要求

**版本**：此结构从 windows 7 开始提供，在 windows 8 及更高版本中已过时。

**标头**： *Ntifs* （包括 Ntifs 或 Ntddk）


## <a name="see-also"></a>另请参阅

[DUAL_OP_LOCK_KEY_ECP_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ifs/dual-oplock-key-ecp-context)

[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)
