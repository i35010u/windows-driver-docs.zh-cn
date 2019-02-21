---
title: EXT\_TDOP\_RELEASE
description: EXT\_TDOP\_释放子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作释放类型化的数据说明。
ms.assetid: 4c2bbc65-a98d-4ee7-bbd0-e30b33c330e0
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
ms.openlocfilehash: 70389f57b224b26e87464c79766a170f65bc1f37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521382"
---
# <a name="exttdoprelease"></a>EXT\_TDOP\_RELEASE


EXT\_TDOP\_版本的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI** ](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作释放类型化的数据说明。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_此子操作的版本。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定的实例[**调试\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff541706)结构释放。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_版本是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明在此特定的设置中指定只有成员的用途。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






