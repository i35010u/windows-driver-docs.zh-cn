---
title: EXT\_TDOP\_OUTPUT\_完整\_值
description: EXT\_TDOP\_OUTPUT\_调试\_请求的完全\_值子操作\_EXT\_类型\_数据\_ANSI 请求操作会打印指定类型化数据的类型和值。
ms.assetid: d64f7a38-c9ae-412f-985b-22115d772116
keywords:
- EXT_TDOP_OUTPUT_FULL_VALUE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_FULL_VALUE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64713167cee17ca71b4208932d49ec6a9fa0dcc4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826430"
---
# <a name="ext_tdop_output_full_value"></a>EXT\_TDOP\_OUTPUT\_完整\_值


EXT\_TDOP\_OUTPUT\_调试\_请求的完全\_值子操作[ **\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作输出指定的类型和值类型化数据。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_OUTPUT\_此子操作的完整\_值。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定将打印其类型名称和值的类型化数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

类型名称和格式化值将发送到调试器引擎的[输出回调](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-input-and-output#output-callbacks)。 EXT\_TDOP\_OUTPUT\_FULL\_值打印有关值的更多详细信息，而不是[**EXT\_TDOP\_OUTPUT\_SIMPLE\_值**](ext-tdop-output-simple-value.md)。 例如，引用指针并同时打印它们指向的值。

EXT\_TDOP\_OUTPUT\_完整\_值是[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






