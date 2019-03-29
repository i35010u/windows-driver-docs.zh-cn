---
title: C30030
description: 警告 C30030 调用内存分配函数并传递一个参数，指示可执行文件的内存。
ms.assetid: D1C8B316-DC04-4B18-A0EB-40833D50B843
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30030
ms.openlocfilehash: b5542a3de5f333824c20d9f2588b5668b3861d66
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348660"
---
# <a name="c30030"></a>C30030


警告 C30030:调用内存分配函数并传递一个参数，指示可执行文件的内存

已禁止\_内存优化\_分配\_UNSAFE

某些 Api 已配置无论内存可执行文件的参数。 此错误指示参数使用结果中可执行文件的非分页池正在分配。 应使用的可用选项之一来请求非可执行文件的内存。

## <a name="span-idfordefectsinvolvingtheparametertypesmmpagepriorityandpooltypespanspan-idfordefectsinvolvingtheparametertypesmmpagepriorityandpooltypespanspan-idfordefectsinvolvingtheparametertypesmmpagepriorityandpooltypespanfor-defects-involving-the-parameter-types-mmpagepriority-and-pooltype"></a><span id="For_defects_involving_the_parameter_types_MM_PAGE_PRIORITY_and_POOL_TYPE"></span><span id="for_defects_involving_the_parameter_types_mm_page_priority_and_pool_type"></span><span id="FOR_DEFECTS_INVOLVING_THE_PARAMETER_TYPES_MM_PAGE_PRIORITY_AND_POOL_TYPE"></span>有关涉及的参数类型的缺陷**MM\_页面\_优先级**并**池\_类型**


使用以下选项之一：

-   指定预处理器定义[池\_NX\_OPTIN\_自动](https://msdn.microsoft.com/library/windows/hardware/hh920390)源/项目设置中。
-   指定预处理器定义[池\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)中，源/项目设置并调用**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** 从驱动程序初始化函数 (**DriverEntry**或**DllInitialize**)。

**请注意**是否要使用的选项[池\_NX\_OPTIN\_自动](https://msdn.microsoft.com/library/windows/hardware/hh920390)或者[池\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)很大程度上取决于哪种平台上您的目标和要进行多少二进制文件。 这两种选项会导致这两种类型更改为您 （由编译器或在运行时） 为其 NX 等效项。 查看详细信息的主题链接。



**请注意**如果以下条件之一为 true，则可能出现的假正警告：
-   驱动程序初始化函数调用另一个调用的函数**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)**
-   要创建**驱动程序\_库**，并指定了[池\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)但没有初始化函数。



-   分配类型更改为非可执行文件类型。

**示例 (池\_NX\_OPTIN\_自动):**

源文件中的以下设置将允许该警告应提供一个可执行文件参数中的 API 调用：

```
C_DEFINES=$(C_DEFINES)
```

源文件中的以下设置可避免此警告：

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN_AUTO=1
```

**示例 (池\_NX\_OPTIN):**

源文件中的以下代码生成警告：

```
C_DEFINES=$(C_DEFINES)
```

源文件中的以下代码可避免此警告：

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

在中**DriverEntry()**、 任何内存分配发生之前：

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;

    ExInitializeDriverRuntime( DrvRtPoolNxOptIn );
…
```

**示例 （更改分配类型）：**

有关**MM\_页面\_优先级**类型可以解决此问题通过添加**MdlMappingNoExecute**优先级类型的标志。 Windows 8 及更高版本才支持此选项。

下面的代码生成警告：

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority);
```

下面的代码可避免此警告：

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority | MdlMappingNoExecute);
```

**示例 (池\_类型)**

有关**池\_类型**可以通过将请求类型更改为的类型的非可执行文件版本来修复此问题的类型。 Windows 8 及更高版本才支持此选项。

下面的代码生成警告：

```
ExAllocatePoolWithTag(NonPagedPool, numberOfBytes, 'xppn');
```

下面的代码可避免此警告：

```
ExAllocatePoolWithTag(NonPagedPoolNx, numberOfBytes, 'xppn');
```

**其他特殊情况：**

已在中的更改[ **ExInitializeNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545301)例程现在可用于指定非可执行文件的非分页缓冲的池内存。 例如，下面的代码生成此警告：

```
ExInitializeNPagedLookasideList(pLookaside,
                NULL,
                NULL,
                0,
                size,
                tag,
                depth);
```

下面的代码可避免此警告：

```
ExInitializeNPagedLookasideList(pLookaside,
                NULL,
                NULL,
                POOL_NX_ALLOCATION,
                size,
                tag,
                depth);
```

## <a name="span-idfordefectsinvolvingpageprotectionsspanspan-idfordefectsinvolvingpageprotectionsspanspan-idfordefectsinvolvingpageprotectionsspanfor-defects-involving-page-protections"></a><span id="For_defects_involving_page_protections_"></span><span id="for_defects_involving_page_protections_"></span><span id="FOR_DEFECTS_INVOLVING_PAGE_PROTECTIONS_"></span>为涉及页保护的缺陷：


某些 Api，可以指定页保护[ **ZwMapViewOfSection** ](https://msdn.microsoft.com/library/windows/hardware/ff566481)就是其中之一。 在这些情况下，使用保护类型的非可执行文件版本。

更改：

-   页\_执行的任何以下替代方法或页\_NOACCESS
-   页\_EXECUTE\_读取到页\_READONLY
-   页\_EXECUTE\_读写到页面\_READWRITE
-   页\_EXECUTE\_WRITECOPY 到页\_WRITECOPY

下面的代码生成警告：

```
Status = ZwMapViewOfSection(   handle,
                NtCurrentProcess(),
                Address,
                0,
                0,
                &SectionOffset,
                Size,
                ViewUnmap,
                MEM_LARGE_PAGES,
                PAGE_EXECUTE_READWRITE
                ); 
```

下面的代码可避免此警告：

```
Status = ZwMapViewOfSection(   handle,
                NtCurrentProcess(),
                Address,
                0,
                0,
                &SectionOffset,
                Size,
                ViewUnmap,
                MEM_LARGE_PAGES,
                PAGE_READWRITE
                ); 
```

## <a name="span-idfordefectsinvolvingcachetypesspanspan-idfordefectsinvolvingcachetypesspanspan-idfordefectsinvolvingcachetypesspanfor-defects-involving-cache-types"></a><span id="For_defects_involving_cache_types_"></span><span id="for_defects_involving_cache_types_"></span><span id="FOR_DEFECTS_INVOLVING_CACHE_TYPES_"></span>为涉及缓存类型的缺陷：


某些 Api 分配内存以及可执行文件的权限取决于缓存类型。 两个此类 api [ **MmAllocateContiguousMemorySpecifyCache** ](https://msdn.microsoft.com/library/windows/hardware/ff554464)并[ **MmAllocateContiguousMemorySpecifyCacheNode**](https://msdn.microsoft.com/library/windows/hardware/ff554469)。 应缓存类型的**MmCached**使用 (请参阅[**内存\_缓存\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff554430))，然后将分配给可执行文件的内存。 若要解决此问题，请选择另一种缓存类型，或如果是必需的内存缓存然后使用 API [ **MmAllocateContiguousNodeMemory**](https://msdn.microsoft.com/library/windows/hardware/jj602795)。

更改：

-   **MmCached**到**MmNonCached**或**MmWriteCombined**如果不需要缓存的内存
-   到 API [ **MmAllocateContiguousNodeMemory** ](https://msdn.microsoft.com/library/windows/hardware/jj602795)是否需要缓存的内存

下面的代码生成警告：

```
MmAllocateContiguousMemorySpecifyCache(       numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmCached,
                                              ); 
```

下面的代码可避免此警告，如果不需要内存缓存：

```
MmAllocateContiguousMemorySpecifyCache(       numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmNonCached,
                                              ); 
```

下面的代码生成警告：

```
MmAllocateContiguousMemorySpecifyCacheNode(   numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmCached,
                                              MM_ANY_NODE_OK
                                              ); 
```

下面的代码可避免此警告，如果是必需的内存缓存：

```
MmAllocateContiguousNodeMemory(       numberOfBytes,
                                      lowestAddress,
                                      highestAddress,
                                      NULL,
                                      PAGE_READWRITE,
                                      MM_ANY_NODE_OK
                                      ); 
```

下面的代码不需要缓存的内存时使用备用 API:

```
MmAllocateContiguousNodeMemory(       numberOfBytes,
                                      lowestAddress,
                                      highestAddress,
                                      NULL,
                                      PAGE_READWRITE | PAGE_NOCACHE,
                                      MM_ANY_NODE_OK
                                      ); 
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**池\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)










