---
title: 调用扩展和扩展函数
description: 调用扩展和扩展函数
ms.assetid: 0582cdc2-7059-42db-878b-28767a6fe850
keywords:
- 调试器引擎 API，调用扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e46d3c5b1e9a244558d6c9a97d176d48c0aec63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367041"
---
# <a name="calling-extensions-and-extension-functions"></a>调用扩展和扩展函数


若要加载扩展库 （或获取已加载的扩展库的句柄），使用[ **AddExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-addextension)。 可以通过卸载扩展库[ **RemoveExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removeextension)。

可以使用调用扩展命令[ **CallExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-callextension)。

### <a name="span-idextensionfunctionsspanspan-idextensionfunctionsspanextension-functions"></a><span id="extension_functions"></span><span id="EXTENSION_FUNCTIONS"></span>扩展函数

*扩展函数*是由扩展库导出的函数。 它们可以使用任何函数原型和调用直接使用 C 函数指针。

它们不是扩展命令且不支持通过调试器命令。 不能远程; 调用扩展函数必须直接调用它们。 因此它们不能从调试客户端使用。 它们只能调用时不远程调试时，或使用智能客户端时，客户端对象是在主机引擎的内部。

扩展函数进行标识的扩展库中"\_EFN\_"附加到其名称。

若要获取扩展函数的指针，请使用[ **GetExtensionFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getextensionfunction)。 此函数指针的类型应与匹配的扩展函数的原型。 现在可以就像在 C 中的任何其他函数指针一样调用扩展函数

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

如果在扩展库中包含以下的扩展函数并将其加载到调试器引擎：

```cpp
HRESULT CALLBACK
_EFN_GetObject(IDebugClient * client, SomeObject * obj);
```

可以使用调用它：

```cpp
typedef ULONG (CALLBACK * GET_OBJECT)(IDebugClient * client, SomeObject * obj);



HRESULT status = S_OK;
GET_OBJECT extFn = NULL;
SomeObject myObj;

if (g_DebugControl->
        GetExtensionFunction(0,
                             "GetObject",
                             (FARPROC *) &extFn ) == S_OK &&
    extFn)
{
    status = (*extFn)(client, &myObj);
}
```

 

 





