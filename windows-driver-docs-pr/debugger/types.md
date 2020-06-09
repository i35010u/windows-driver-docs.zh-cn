---
title: 类型
description: 类型
ms.assetid: 234f4f36-ccd3-426a-a361-33727e9ece5a
keywords:
- 符号，类型
- types
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ae852959fd0d618192a0ac70d33db2827dd8a97
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533826"
---
# <a name="types"></a>类型


## <span id="ddk_types_dbx"></span><span id="DDK_TYPES_DBX"></span>


模块的符号文件中的类型信息由两部分信息标识：类型 ID 和该类型所属的模块的基址。 以下方法可用于查找类型 ID：

-   [**GetTypeId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-gettypeid)返回给定类型名称的类型 ID。

-   [**GetSymbolTypeId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymboltypeid)返回具有给定名称的符号类型的类型 ID。

-   [**GetOffsetTypeId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getoffsettypeid)返回在给定位置找到的符号的类型 ID。

类型的名称和大小分别由[**GetTypeName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-gettypename)和[**GetTypeSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-gettypesize)返回。

以下便利方法可用于在目标的物理内存和虚拟内存中读取和写入类型化数据：

[**ReadTypedDataPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-readtypeddataphysical)

[**WriteTypedDataPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-writetypeddataphysical)

[**ReadTypedDataVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-readtypeddatavirtual)

[**WriteTypedDataVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-writetypeddatavirtual)

### <a name="span-idprinting_typed_dataspanspan-idprinting_typed_dataspanprinting-typed-data"></a><span id="printing_typed_data"></span><span id="PRINTING_TYPED_DATA"></span>打印类型化数据

若要设置类型化数据的格式并将其发送到输出回调，请将[*OutputTypedDataPhysical*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-outputtypeddataphysical)和[*OutputTypedDataVirtual*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-outputtypeddatavirtual)分别用于目标物理和虚拟内存中的数据。

[**DEBUG \_ TYPEOPTS \_ XXX**](debug-typeopts-xxx.md)中描述的类型选项会影响引擎在将类型化数据发送到输出回调之前如何设置其格式。

可以使用[**AddTypeOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-addtypeoptions)打开类型选项，并通过使用[**RemoveTypeOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-removetypeoptions)将其关闭。

[**GetTypeOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-gettypeoptions)返回当前的类型选项。 若要同时设置所有类型选项，请使用[**SetTypeOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-settypeoptions)。

### <a name="span-idinterpreting_raw_data_using_type_informationspanspan-idinterpreting_raw_data_using_type_informationspaninterpreting-raw-data-using-type-information"></a><span id="interpreting_raw_data_using_type_information"></span><span id="INTERPRETING_RAW_DATA_USING_TYPE_INFORMATION"></span>使用类型信息解释原始数据

调试器引擎 API 支持解释类型化数据。 这提供了一种方法来遍历目标上的对象层次结构，包括查找结构的成员、取消引用指针以及查找数组元素。

类型化的数据由[**调试 \_ 类型化 \_ 数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)结构的实例描述，表示目标强制转换为特定类型的内存区域。 [**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)**请求**操作用于操作这些实例。 可以将它们初始化为表达式的结果，或将内存的区域强制转换为指定类型。 有关调试 \_ 请求 \_ EXT \_ 类型化数据 ANSI 请求操作支持的所有子操作的列表 \_ \_ ，请参阅[**EXT \_ TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)。 **Request**

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关输出回调的详细信息，请参阅[输入和输出](using-input-and-output.md)。

 

 





