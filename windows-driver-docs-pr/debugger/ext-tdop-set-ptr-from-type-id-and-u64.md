---
title: EXT\_TDOP\_设置\_PTR\_从\_类型\_ID\_和\_U64
description: EXT\_TDOP\_设置\_PTR\_，\_\_类型\_\_\_类型\_\_类型\_@no__ 类型数据t_12_ ANSI 请求操作创建一个类型化的数据说明，该说明表示指向具有指定类型的指定内存位置的指针。
ms.assetid: 1ca61962-718e-4cbd-8e16-f87e0c9ec9af
keywords:
- EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64 Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d93f97feff23ab1e89fea68cb84694550e26e85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838758"
---
# <a name="ext_tdop_set_ptr_from_type_id_and_u64"></a>EXT\_TDOP\_设置\_PTR\_从\_类型\_ID\_和\_U64


EXT\_TDOP\_设置\_PTR\_，\_\_类型\_\_\_类型\_\_类型\_@no__ 类型[**数据t_14_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作创建一个类型化的数据说明，该说明表示指向具有指定类型的指定内存位置的指针。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_将\_PTR\_从\_类型\_ID\_和\_U64 设置为此子操作。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定用于描述类型化数据的值所在的目标内存的位标志。 有关这些标志的详细信息，请参阅[**EXT\_类型化的\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定类型和内存位置。 可以手动创建并填充所需成员的[**调试\_类型\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)结构的此实例。 使用以下成员：

<span id="ModBase"></span><span id="modbase"></span><span id="MODBASE"></span>**ModBase**  
指定包含类型的模块基址的目标虚拟内存中的位置。

<span id="Offset"></span><span id="offset"></span><span id="OFFSET"></span>**抵销**  
指定目标的数据内存中的位置。 **偏移量**是虚拟内存地址，除非**标志**中存在指定该**偏移量**是物理内存地址的标志。

<span id="TypeId"></span><span id="typeid"></span><span id="TYPEID"></span>**TypeId**  
指定类型的类型 ID。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收表示指向内存位置和类型的指针的类型化数据说明。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_设置\_PTR\_从\_类型\_ID\_和\_U64 是[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






