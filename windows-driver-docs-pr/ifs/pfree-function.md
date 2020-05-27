---
title: PFREE_FUNCTION 函数指针
description: PFREE_FUNCTION 类型化例程可由文件系统旧筛选器驱动程序注册为筛选器的 FreeCallback 回调例程。
ms.assetid: 291b57d9-3bef-4acb-a571-86b67a03cd08
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
ms.openlocfilehash: e599ba76e3e39f307f00587e0c3217abd6e8058b
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852311"
---
# <a name="pfree_function-function-pointer"></a>PFREE_FUNCTION 函数指针

**PFREE_FUNCTION**类型化例程可由文件系统旧筛选器驱动程序注册为筛选器的*FreeCallback*回调例程。 文件系统通过使用[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)删除文件上下文对象，或使用[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)删除流上下文对象时，文件系统将调用*FreeCallback* 。

必须使用**FREE_FUNCTION**类型来声明回调例程。 有关详细信息，请参阅 "备注" 部分中的示例。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef VOID ( *FreeCallback)(
  _In_ PVOID Buffer
);
```

## <a name="parameters"></a>参数

*缓冲区* \[中\]  
指向要释放的[**FSRTL_PER_FILE_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547352)或[**FSRTL_PER_STREAM_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357)结构的指针。

## <a name="return-value"></a>返回值
------------

无

## <a name="remarks"></a>备注

当文件系统泪水文件的每个文件上下文对象时，它必须调用[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)。 此例程调用与文件关联的所有每文件上下文结构的*FreeCallback*例程。 此回调例程必须释放用于[**FSRTL_PER_FILE_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547352)对象的任何内存以及任何关联的上下文信息。 这也适用于调用[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)时的每个流上下文， *FreeCallback*将释放用于[**FSRTL_PER_STREAM_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357)对象的内存。

有关如何在调用*FreeCallback*期间同步对每个文件上下文对象或按流上下文对象的访问的备注，请参阅[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)和[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)。

> [!NOTE]
> *FreeCallback*例程无法以递归方式向下调用文件系统或获取任何文件系统资源。

若要定义名为*MyFreeFunction*的*FreeCallback*回调函数，必须先提供[静态驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)器（SDV）和其他验证工具需要的函数声明，如下所示：

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

|   |   |
| - | - |
| 目标平台 | 桌面型 |
| 版本 | 可从与 windows Vista 开始使用。 |
| Header | Wdm （包括 Wdm 或 Ntddk） |
| IRQL | <= APC_LEVEL |

## <a name="see-also"></a>另请参阅

[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)

[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)

[**FSRTL_PER_FILE_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547352)

[**FSRTL_PER_STREAM_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357)

[跟踪旧文件系统筛选器驱动程序中的按文件上下文](https://docs.microsoft.com/windows-hardware/drivers/ifs/tracking-per-file-context-in-a-legacy-file-system-filter-driver)

[跟踪旧文件系统筛选器驱动程序中的按流上下文](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-streams--stream-contexts--and-per-stream-contexts
)
