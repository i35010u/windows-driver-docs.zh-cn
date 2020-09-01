---
title: '\_ \_ \_ \_ 类型 \_ ID \_ 和 \_ U64 中的 EXT TDOP 集'
description: '\_ \_ \_ \_ \_ \_ 调试请求的类型 ID 和 U64 子操作的 ext TDOP 集 \_ \_ \_ ext \_ 类型化的 \_ 数据 \_ ANSI 请求操作将从数据类型和内存位置创建类型化的数据说明。'
ms.assetid: 5b1ee241-6f35-4bbf-b4e0-3cefa5a39dde
keywords:
- EXT_TDOP_SET_FROM_TYPE_ID_AND_U64 Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_FROM_TYPE_ID_AND_U64
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25098dc2631306a192805da1afed529f9a63f5bc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206814"
---
# <a name="ext_tdop_set_from_type_id_and_u64"></a>\_ \_ \_ \_ 类型 \_ ID \_ 和 \_ U64 中的 EXT TDOP 集


\_ \_ \_ \_ \_ \_ 调试请求的类型 ID 和 U64 子操作的 ext TDOP 集 \_ [** \_ \_ ext \_ 类型化的 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作将从数据类型和内存位置创建类型化的数据说明。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
\_对于此子操作，请将设置为 TDOP \_ \_ \_ 类型 \_ ID \_ 和 \_ U64 中的扩展。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定用于描述类型化数据的值所在的目标内存的位标志。 有关这些标志的详细信息，请参阅 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定类型和内存位置。 可以手动创建并填充所需成员的 [**调试 \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data) 结构的此实例。 使用以下成员：

<span id="ModBase"></span><span id="modbase"></span><span id="MODBASE"></span>**ModBase**  
指定包含类型的模块基址的目标虚拟内存中的位置。

<span id="Offset"></span><span id="offset"></span><span id="OFFSET"></span>**抵销**  
指定目标的数据内存中的位置。 **偏移量** 是虚拟内存地址，除非 **标志** 中存在指定该 **偏移量** 是物理内存地址的标志。

<span id="TypeId"></span><span id="typeid"></span><span id="TYPEID"></span>**TypeId**  
指定类型的类型 ID。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收类型化数据说明。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

\_ \_ 类型 ID 和 U64 中的 ext TDOP 集 \_ \_ \_ \_ \_ 是[**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

