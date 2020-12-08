---
title: PFREE_FUNCTION 函数指针
description: PFREE_FUNCTION 类型化例程可由文件系统旧筛选器驱动程序注册为筛选器的 FreeCallback 回调例程。
keywords:
- PFREE_FUNCTION 函数指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FreeCallback
api_location:
- wdm.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd2a91ba42d7a9c4e8d975ba0a7e4ebeb392cede
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836447"
---
# <a name="pfree_function-function-pointer"></a>PFREE_FUNCTION 函数指针

**PFREE_FUNCTION** 类型化例程可由文件系统旧筛选器驱动程序注册为筛选器的 *FreeCallback* 回调例程。 文件系统通过使用 [**FsRtlTeardownPerFileContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperfilecontexts)删除文件上下文对象，或使用 [**FsRtlTeardownPerStreamContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperstreamcontexts)删除流上下文对象时，文件系统将调用 *FreeCallback* 。

必须使用 **FREE_FUNCTION** 类型来声明回调例程。 有关详细信息，请参阅 "备注" 部分中的示例。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef VOID ( *FreeCallback)(
  _In_ PVOID Buffer
);
```

## <a name="parameters"></a>参数

*缓冲区* \[中\]  
指向要释放的 [**FSRTL_PER_FILE_CONTEXT**](/previous-versions/ff547352(v=vs.85)) 或 [**FSRTL_PER_STREAM_CONTEXT**](/previous-versions/ff547357(v=vs.85)) 结构的指针。

## <a name="return-value"></a>返回值
------------

无

## <a name="remarks"></a>备注

当文件系统泪水文件的每个文件上下文对象时，它必须调用 [**FsRtlTeardownPerFileContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperfilecontexts)。 此例程调用与文件关联的所有每文件上下文结构的 *FreeCallback* 例程。 此回调例程必须释放用于 [**FSRTL_PER_FILE_CONTEXT**](/previous-versions/ff547352(v=vs.85)) 对象的任何内存以及任何关联的上下文信息。 这也适用于调用 [**FsRtlTeardownPerStreamContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperstreamcontexts) 时的每个流上下文， *FreeCallback* 将释放用于 [**FSRTL_PER_STREAM_CONTEXT**](/previous-versions/ff547357(v=vs.85)) 对象的内存。

有关如何在调用 *FreeCallback* 期间同步对每个文件上下文对象或按流上下文对象的访问的备注，请参阅 [**FsRtlTeardownPerFileContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperfilecontexts) 和 [**FsRtlTeardownPerStreamContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperstreamcontexts)。

> [!NOTE]
> *FreeCallback* 例程无法以递归方式向下调用文件系统或获取任何文件系统资源。

若要定义名为 *MyFreeFunction* 的 *FreeCallback* 回调函数，必须先提供 [静态驱动程序验证](../devtest/static-driver-verifier.md)器 (SDV) 和其他验证工具需要的函数声明，如下所示：

```cpp
FREE_FUNCTION MyFreeFunction;
```

然后按如下所示实现回调函数：

```cpp
VOID
 MyFreeFunction (
 __in PVOID Buffer
    )
  {...}
```

## <a name="requirements"></a>要求

**目标平台**：桌面

**版本**：从与 windows Vista 开始可用。

**标头**： wdm .h (包括 Wdm 或 Ntddk) 

**IRQL**： <= APC_LEVEL


## <a name="see-also"></a>请参阅

[**FsRtlTeardownPerFileContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperfilecontexts)

[**FsRtlTeardownPerStreamContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperstreamcontexts)

[**FSRTL_PER_FILE_CONTEXT**](/previous-versions/ff547352(v=vs.85))

[**FSRTL_PER_STREAM_CONTEXT**](/previous-versions/ff547357(v=vs.85))

[跟踪旧文件系统筛选器驱动程序中的 Per-File 上下文](./tracking-per-file-context-in-a-legacy-file-system-filter-driver.md)

[跟踪旧文件系统筛选器驱动程序中的 Per-Stream 上下文](./file-streams--stream-contexts--and-per-stream-contexts.md
)
