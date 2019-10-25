---
title: EXT\_TDOP\_获取\_取消引用
description: EXT\_TDOP\_获取调试\_请求\_取消引用子操作\_类型\_数据\_ANSI 请求操作取消引用指针并返回它所指向的值。
ms.assetid: 0b5eed03-4241-4038-8950-12c82c2d086f
keywords:
- EXT_TDOP_GET_DEREFERENCE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_DEREFERENCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bef65e09540480d41536f659e46b4c92be52abd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826489"
---
# <a name="ext_tdop_get_dereference"></a>EXT\_TDOP\_获取\_取消引用


EXT\_TDOP\_获取调试\_请求\_取消引用子操作[ **\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作取消引用指针并返回它所指向的值自。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_为此子操作获取\_取消引用。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定要取消引用的指针。 **InData**还可以指定数组，在这种情况下，将返回数组中的第一个元素。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收指向的值。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_获取\_取消引用是[**ext\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






