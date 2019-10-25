---
title: EXT\_TDOP\_获取\_指针\_到
description: EXT\_TDOP\_获取\_指针\_到调试\_请求的子操作\_类型\_数据\_ANSI 请求操作返回一个表示指向的指针的新类型化数据说明。指定的类型化数据。
ms.assetid: 05db8e07-b94f-4cf3-b01b-a918b737ecf4
keywords:
- EXT_TDOP_GET_POINTER_TO Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_POINTER_TO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7ce87048a728ce33c0d722741499d34dd583230
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826450"
---
# <a name="ext_tdop_get_pointer_to"></a>EXT\_TDOP\_获取\_指针\_到


EXT\_TDOP\_获取\_指针\_到调试\_请求的子操作[ **\_\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回一个新的类型化数据说明，表示指向指定类型化数据的指针。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_为此子操作获取\_指针\_。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定指针返回到的原始类型化数据说明。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收一个类型化的数据说明，该说明表示指向由**InData**指定的类型化数据的指针。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_获取\_指针\_是[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






