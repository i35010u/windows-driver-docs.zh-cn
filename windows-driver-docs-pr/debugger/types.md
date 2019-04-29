---
title: 类型
description: 类型
ms.assetid: 234f4f36-ccd3-426a-a361-33727e9ece5a
keywords:
- 符号类型
- 类型
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b83cfdad72ec12d5f6beec0819dac1ed40f0605
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380783"
---
# <a name="types"></a>类型


## <span id="ddk_types_dbx"></span><span id="DDK_TYPES_DBX"></span>


模块的符号文件的类型信息由两条信息： 类型 ID 和该类型所属的模块的基址。 可以使用以下方法，若要查找类型 ID:

-   [**GetTypeId** ](https://msdn.microsoft.com/library/windows/hardware/ff549376)返回给定的类型名称的类型 ID。

-   [**GetSymbolTypeId** ](https://msdn.microsoft.com/library/windows/hardware/ff549173)返回具有给定名称的符号的类型的类型 ID。

-   [**GetOffsetTypeId** ](https://msdn.microsoft.com/library/windows/hardware/ff548062)返回在给定位置中找到的符号的类型 ID。

通过返回的名称和类型的大小[ **GetTypeName** ](https://msdn.microsoft.com/library/windows/hardware/ff549408)并[ **GetTypeSize**](https://msdn.microsoft.com/library/windows/hardware/ff549457)分别。

以下的简便方法可用于读取和写入目标的物理和虚拟内存中的类型化的数据：

[**ReadTypedDataPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff554344)

[**WriteTypedDataPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff561463)

[**ReadTypedDataVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff554345)

[**WriteTypedDataVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff561466)

### <a name="span-idprintingtypeddataspanspan-idprintingtypeddataspanprinting-typed-data"></a><span id="printing_typed_data"></span><span id="PRINTING_TYPED_DATA"></span>打印类型化数据

设置类型化的数据的格式并将其发送到输出回调，请使用[ *OutputTypedDataPhysical* ](https://msdn.microsoft.com/library/windows/hardware/ff553269)并[ *OutputTypedDataVirtual* ](https://msdn.microsoft.com/library/windows/hardware/ff553274)为目标的物理和虚拟内存中的数据分别。

类型选项中所述[**调试\_TYPEOPTS\_XXX** ](https://msdn.microsoft.com/library/windows/hardware/ff541712)影响引擎如何格式化类型化的数据发送到输出回调之前。

类型选项可能会使用开启[ **AddTypeOptions**](https://msdn.microsoft.com/library/windows/hardware/ff537949)，并通过使用关闭[ **RemoveTypeOptions**](https://msdn.microsoft.com/library/windows/hardware/ff554551)。

[**GetTypeOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff549428)返回当前类型选项。 若要同时设置所有类型选项，请使用[ **SetTypeOptions**](https://msdn.microsoft.com/library/windows/hardware/ff556874)。

### <a name="span-idinterpretingrawdatausingtypeinformationspanspan-idinterpretingrawdatausingtypeinformationspaninterpreting-raw-data-using-type-information"></a><span id="interpreting_raw_data_using_type_information"></span><span id="INTERPRETING_RAW_DATA_USING_TYPE_INFORMATION"></span>解释使用类型信息的原始数据

调试器引擎 API 支持解释类型的数据。 这提供了一种方法来遍历目标，包括查找的结构的成员、 取消引用指针，以及查找数组元素上的对象层次结构。

类型化的数据由的实例来描述[**调试\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff541706)结构并表示强制转换为特定类型的目标上的内存的区域。 [**调试\_请求\_EXT\_类型化\_数据\_ANSI**](https://msdn.microsoft.com/library/windows/hardware/ff541547)**请求**使用操作若要操作这些实例。 它们可以初始化为结果的表达式或被强制转换为指定类型的内存的区域。 有关的所有子操作的列表的调试\_请求\_EXT\_类型化\_数据\_ANSI**请求**操作支持，请参阅[ **EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

输出回调的详细信息，请参阅[输入和输出](using-input-and-output.md)。

 

 





