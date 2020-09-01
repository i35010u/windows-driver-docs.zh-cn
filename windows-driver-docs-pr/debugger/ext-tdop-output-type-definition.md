---
title: EXT \_ TDOP \_ 输出 \_ 类型 \_ 定义
description: '\_DEBUG 请求的 ext TDOP \_ 输出 \_ 类型 \_ 定义子操作 \_ \_ Ext \_ 类型化 \_ \_ 的数据 ANSI 请求操作将为指定的类型化数据打印类型的定义。'
ms.assetid: 88e97066-f471-4e6c-9b9b-369f31da5bde
keywords:
- EXT_TDOP_OUTPUT_TYPE_DEFINITION Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_TYPE_DEFINITION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44e7340fd1af809fd8f3e665d0919eabbae80a93
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217380"
---
# <a name="ext_tdop_output_type_definition"></a>EXT \_ TDOP \_ 输出 \_ 类型 \_ 定义


\_DEBUG 请求的 ext TDOP \_ 输出 \_ 类型 \_ 定义子操作[** \_ \_ ext \_ 类型化的 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作将为指定的类型化数据打印类型的定义。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT \_ TDOP \_ \_ \_ 此子操作的输出类型定义。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定将输出其类型定义的类型化数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

对类型的定义进行格式化，并将其发送到调试器引擎的 [输出回调](./using-input-and-output.md#output-callbacks)。

EXT \_ TDOP \_ OUTPUT \_ TYPE \_ DEFINITION 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

