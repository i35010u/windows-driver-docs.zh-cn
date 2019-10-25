---
title: 调用扩展和扩展函数
description: 调用扩展和扩展函数
ms.assetid: 0582cdc2-7059-42db-878b-28767a6fe850
keywords:
- 调试器引擎 API，调用扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: daa6f04e85c275a779b876ca01242b4c2f5519a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837832"
---
# <a name="calling-extensions-and-extension-functions"></a>调用扩展和扩展函数


若要加载扩展库（或获取已加载的扩展库的句柄），请使用[**AddExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-addextension)。 可以使用[**RemoveExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removeextension)卸载扩展库。

可以使用[**CallExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-callextension)调用扩展命令。

### <a name="span-idextension_functionsspanspan-idextension_functionsspanextension-functions"></a><span id="extension_functions"></span><span id="EXTENSION_FUNCTIONS"></span>扩展函数

*扩展函数*是由扩展库导出的函数。 它们可以使用任何函数原型，并使用 C 函数指针直接调用。

它们不是扩展命令，也不能通过调试器命令获得。 不能远程调用扩展函数;必须直接调用它们。 因此，它们不能用于调试客户端。 仅当客户端对象位于主机引擎内时，才可以调用它们-如果不进行远程调试或使用智能客户端。

扩展函数在扩展库中通过 "\_EFN\_" 前面的名称进行标识。

若要获取指向扩展函数的指针，请使用[**GetExtensionFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getextensionfunction)。 此函数指针的类型应与 extension 函数的原型匹配。 现在，可以像在 C 中的任何其他函数指针一样调用扩展函数。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>实例

如果以下扩展函数包含在扩展库中并加载到调试器引擎中：

```cpp
HRESULT CALLBACK
_EFN_GetObject(IDebugClient * client, SomeObject * obj);
```

可以使用以下方法调用它：

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

 

 





