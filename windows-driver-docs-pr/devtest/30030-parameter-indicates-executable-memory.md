---
title: C30030
description: 警告 C30030 调用内存分配函数并传递指示可执行文件内存的参数。
ms.assetid: D1C8B316-DC04-4B18-A0EB-40833D50B843
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30030
ms.openlocfilehash: 7f5128021f75e46114b6209b81e1b80486e7b1a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840310"
---
# <a name="c30030"></a>C30030


警告 C30030：调用内存分配函数并传递指示可执行内存的参数

禁止\_内存\_分配\_不安全

某些 Api 有一些参数，可用于配置内存是否可执行。 此错误表示使用的参数会导致分配可执行文件非分页池。 你应使用一个可用的选项来请求不可执行的内存。

## <a name="span-idfor_defects_involving_the_parameter_types_mm_page_priority_and_pool_typespanspan-idfor_defects_involving_the_parameter_types_mm_page_priority_and_pool_typespanspan-idfor_defects_involving_the_parameter_types_mm_page_priority_and_pool_typespanfor-defects-involving-the-parameter-types-mm_page_priority-and-pool_type"></a><span id="For_defects_involving_the_parameter_types_MM_PAGE_PRIORITY_and_POOL_TYPE"></span><span id="for_defects_involving_the_parameter_types_mm_page_priority_and_pool_type"></span><span id="FOR_DEFECTS_INVOLVING_THE_PARAMETER_TYPES_MM_PAGE_PRIORITY_AND_POOL_TYPE"></span>对于涉及参数类型 MM 的缺陷 **\_页面\_优先级**和**池\_类型**


使用以下选项之一：

-   在源/项目设置中[\_NX\_OPTIN\_自动](https://docs.microsoft.com/windows-hardware/drivers/kernel/multiple-binary-opt-in-pool-nx-optin-auto)指定预处理器定义池。
-   在源/项目设置中[\_NX\_OPTIN](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin)指定预处理器定义池，**并从驱动程序初始化函数（** **DriverEntry**或**DllInitialize**）。

**注意** 选择是使用[池\_nx\_OPTIN\_自动](https://docs.microsoft.com/windows-hardware/drivers/kernel/multiple-binary-opt-in-pool-nx-optin-auto)还是[池\_NX\_OPTIN](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin) ，这在很大程度上取决于您所面向的平台和要进行的二进制文件的数量。 这两个选项都会导致这两种类型（由编译器或运行时）更改为其 NX 等效项。 有关详细信息，请参阅主题链接。



**注意** 如果满足以下条件之一，则可能会出现误报警告：
-   驱动程序初始化函数调用另一个调用**ExInitializeDriverRuntime （*DrvRtPoolNxOptIn*）** 的函数
-   正在创建 **\_库的驱动程序**，并且已指定了[池\_NX\_OPTIN](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin) ，但没有初始化函数。



-   将分配类型更改为不可执行的类型。

**示例（POOL\_NX\_OPTIN\_自动）：**

源文件中的以下设置将允许在 API 调用中提供可执行参数的警告：

```
C_DEFINES=$(C_DEFINES)
```

源文件中的以下设置可避免出现此警告：

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN_AUTO=1
```

**示例（POOL\_NX\_OPTIN）：**

源文件中的以下代码生成警告：

```
C_DEFINES=$(C_DEFINES)
```

源文件中的以下代码可避免此警告：

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

在**DriverEntry （）** 中，在发生任何内存分配之前：

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

**示例（更改分配类型）：**

对于**MM\_页面\_优先级**类型，可以通过将**MdlMappingNoExecute**标志添加到优先级类型来解决此问题。 只有 Windows 8 及更高版本支持此版本。

下面的代码生成一个警告：

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority);
```

下面的代码可避免出现此警告：

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority | MdlMappingNoExecute);
```

**示例（池\_类型）**

对于**池\_类型**类型，可以通过将请求类型更改为类型的不可执行版本来解决此问题。 只有 Windows 8 及更高版本支持此版本。

下面的代码生成一个警告：

```
ExAllocatePoolWithTag(NonPagedPool, numberOfBytes, 'xppn');
```

下面的代码可避免出现此警告：

```
ExAllocatePoolWithTag(NonPagedPoolNx, numberOfBytes, 'xppn');
```

**其他特殊情况：**

[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)例程发生了变化，现在可以指定不可执行的非分页池内存。 例如，下面的代码将生成此警告：

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

## <a name="span-idfor_defects_involving_page_protections_spanspan-idfor_defects_involving_page_protections_spanspan-idfor_defects_involving_page_protections_spanfor-defects-involving-page-protections"></a><span id="For_defects_involving_page_protections_"></span><span id="for_defects_involving_page_protections_"></span><span id="FOR_DEFECTS_INVOLVING_PAGE_PROTECTIONS_"></span>对于涉及页面保护的缺陷：


某些 Api 允许你指定页面保护， [**ZwMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)是其中之一。 在这些情况下，请使用保护类型的不可执行版本。

转

-   页面\_执行到以下任意替代或页面\_NOACCESS
-   页\_执行\_读取到页\_READONLY
-   页\_执行\_READWRITE 到页\_READWRITE
-   页\_\_WRITECOPY\_WRITECOPY

下面的代码生成一个警告：

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

## <a name="span-idfor_defects_involving_cache_types_spanspan-idfor_defects_involving_cache_types_spanspan-idfor_defects_involving_cache_types_spanfor-defects-involving-cache-types"></a><span id="For_defects_involving_cache_types_"></span><span id="for_defects_involving_cache_types_"></span><span id="FOR_DEFECTS_INVOLVING_CACHE_TYPES_"></span>有关涉及缓存类型的缺陷：


某些 Api 使用依赖于缓存类型的可执行权限来分配内存。 这两个 Api 是[**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)和[**MmAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycachenode)。 如果要使用**MmCached**的缓存类型（请参阅[**内存\_缓存\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_memory_caching_type)），则将分配可执行内存。 若要解决此问题，请选择其他缓存类型，或者如果需要缓存的内存，则使用 API [**MmAllocateContiguousNodeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousnodememory)。

转

-   **MmCached**到**MmNonCached**或**MmWriteCombined** （如果不需要缓存的内存）
-   如果需要缓存内存，则为要[**MmAllocateContiguousNodeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousnodememory)的 API

下面的代码生成一个警告：

```
MmAllocateContiguousMemorySpecifyCache(       numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmCached,
                                              ); 
```

如果不需要缓存内存，以下代码可避免此警告：

```
MmAllocateContiguousMemorySpecifyCache(       numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmNonCached,
                                              ); 
```

下面的代码生成一个警告：

```
MmAllocateContiguousMemorySpecifyCacheNode(   numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmCached,
                                              MM_ANY_NODE_OK
                                              ); 
```

如果需要缓存内存，以下代码可避免此警告：

```
MmAllocateContiguousNodeMemory(       numberOfBytes,
                                      lowestAddress,
                                      highestAddress,
                                      NULL,
                                      PAGE_READWRITE,
                                      MM_ANY_NODE_OK
                                      ); 
```

如果不需要缓存内存，以下代码将使用替代 API：

```
MmAllocateContiguousNodeMemory(       numberOfBytes,
                                      lowestAddress,
                                      highestAddress,
                                      NULL,
                                      PAGE_READWRITE | PAGE_NOCACHE,
                                      MM_ANY_NODE_OK
                                      ); 
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**池\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)










