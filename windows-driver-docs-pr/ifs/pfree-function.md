---
title: PFREE\_函数函数指针
description: PFREE\_函数键入例程可以注册的文件系统旧筛选器驱动程序，因为筛选器的 FreeCallback 回调例程。
ms.assetid: 291b57d9-3bef-4acb-a571-86b67a03cd08
keywords:
- PFREE_FUNCTION 函数指针可安装文件系统驱动程序
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
ms.openlocfilehash: 1944414572ba8d944743ecbcd9c14feccd774321
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366786"
---
# <a name="pfreefunction-function-pointer"></a>PFREE\_函数函数指针


一个**PFREE\_函数**可通过文件系统旧筛选器驱动程序作为筛选器的注册类型化的例程*FreeCallback*回调例程。 文件系统调用*FreeCallback*在文件系统中删除通过使用文件上下文对象[ **FsRtlTeardownPerFileContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547290)或删除的流上下文对象使用[ **FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)。

必须通过使用声明回调例程**免费\_函数**类型。 有关详细信息，请参阅备注部分中的示例。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef VOID ( *FreeCallback)(
  _In_ PVOID Buffer
);
```

<a name="parameters"></a>Parameters
----------

*缓冲区*\[中\]  
一个指向[ **FSRTL\_每\_文件\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff547352)或[ **FSRTL\_每\_流\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff547357)要释放的结构。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

当文件系统停止每个文件的文件上下文对象，它必须调用[ **FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)。 此例程调用*FreeCallback*与文件关联的每个文件的所有上下文结构的例程。 此回调例程必须释放所用的任何内存[ **FSRTL\_每\_文件\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff547352)对象及所有关联的上下文信息。 这也是每个流上下文的情况时[ **FsRtlTeardownPerStreamContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547295)调用并*FreeCallback*将释放内存用于[ **FSRTL\_出差\_流\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff547357)对象。

有关同步每个文件上下文对象，或以每个流在调用上下文对象对访问权限的备注*FreeCallback*，请参阅[ **FsRtlTeardownPerFileContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547290)并[ **FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)。

&gt; \[!请注意\] &gt; *FreeCallback*例程不能以递归方式调用到文件系统故障或获取任何文件系统资源。

 

若要定义*FreeCallback*回调函数名为*MyFreeFunction*，你必须首先提供的函数声明的[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier) (SDV) 和其他验证工具需要，按如下所示：

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

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Version</p></td>
<td align="left"><p>可用的起始 withWindows Vista。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Wdm.h 中 （包括 wdm.h 中或 Ntddk.h）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)

[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)

[**FSRTL\_PER\_FILE\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547352)

[**FSRTL\_PER\_STREAM\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357)

[跟踪每个文件中的旧文件系统筛选器驱动程序的上下文](https://docs.microsoft.com/windows-hardware/drivers/ifs/tracking-per-file-context-in-a-legacy-file-system-filter-driver)

[跟踪每个 Stream 上下文中的旧文件系统筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/tracking-per-stream-context-in-a-legacy-file-system-filter-driver)

 

 






