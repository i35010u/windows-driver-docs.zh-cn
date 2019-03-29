---
title: WIA 错误处理程序返回值
description: WIA 错误处理程序返回值
ms.assetid: 9b8efcd7-e767-4344-b3a1-96b1898e102f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60c95e657c3bfe103c6b0983d34423d333d309eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562473"
---
# <a name="wia-error-handler-return-values"></a>WIA 错误处理程序返回值


所有的错误处理程序必须遵守有关它们的返回值的规则数。

以下是所有有效的返回值：

<a href="" id="s-ok"></a>S\_确定  
已成功处理设备状态代码。 将调用没有更多的错误处理程序。

发生错误状态代码 （模式对话框），这意味着，采取适当的措施纠正 ADF 纸等错误。

如果信息状态代码，这只意味着执行相应的操作来为用户提供一个无模式对话框和不应将该设备的消息转发到任何其他错误处理程序下的行。

<a href="" id="wia-status-not-handled"></a>WIA\_状态\_不\_已处理  
未不采取任何操作来处理向用户的错误或报表状态。 将调用下一个处理程序 （如果有） 列表中。

这应该是错误处理程序的默认返回值。

<a href="" id="s-false"></a>S\_FALSE  
用户取消了处理程序的无模式对话框从传输。 此返回值可以由无论设备状态代码是错误处理程序返回的任意位置 (已处理的、 未处理状态，错误，或信息性)。

<a href="" id="other-error-codes"></a>其他错误代码  
如果设备错误无法恢复，或者用户选择停止传输响应显示模式对话框，错误处理程序应返回自身的设备状态代码 （请参阅示例部分中的示例）。 当然，这意味着错误处理程序无法处理的设备状态代码。

此外，错误处理程序必须一致地处理设备状态代码。 也就是说，不能选择错误处理程序的实例来处理状态代码 WIA\_状态\_XYZ (或 WIA\_错误\_XYZ) 在时间 t0，但后来无法在 t1 时间对其进行处理。

下面的代码是无效的错误处理程序的示例：

```cpp
STDMETHODIMP
CErrHandler::ReportStatus(
    IN  LONG        lFlags,
    IN  HWND        hwndParent,
    IN  IWiaItem2   *pWiaItem2,
    IN  HRESULT     hrStatus,
    IN  LONG        lPercentComplete)
{
    HRESULT hr = WIA_STATUS_NOT_HANDLED;
    if ((hrStatus == WIA_ERROR_PAPER_JAM) && HandleMessageNow())
    {
        ...
    }
    return hr;
}
```

删除*HandleMessageNow*例程会使这成为有效的错误处理程序。

 

 




