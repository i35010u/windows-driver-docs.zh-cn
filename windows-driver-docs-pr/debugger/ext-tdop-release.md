---
title: 扩展 \_ TDOP \_ 版本
description: '\_调试请求的 ext TDOP \_ RELEASE 子操作在类型化的 \_ \_ \_ \_ 数据 \_ ANSI 请求操作中，释放了类型化的数据说明。'
keywords:
- EXT_TDOP_RELEASE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_RELEASE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0aa4b47c95b01e1495e9127a0066aba4194134c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840217"
---
# <a name="ext_tdop_release"></a>扩展 \_ TDOP \_ 版本


\_调试请求的 ext TDOP \_ RELEASE 子操作在 [**类型化的 \_ \_ \_ \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作中，释放了类型化的数据说明。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
\_ \_ 此子操作的 TDOP 版本设置为 EXT。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定要释放的 [**调试 \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data) 结构的实例。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ RELEASE 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明仅指定此特定设置中的成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

