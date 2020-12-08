---
title: WIA 错误处理程序返回值
description: WIA 错误处理程序返回值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecbb2e64b7fe11636434ba058ad67f09cc69ea7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820229"
---
# <a name="wia-error-handler-return-values"></a>WIA 错误处理程序返回值


所有错误处理程序都必须遵循有关其返回值的多个规则。

下面是所有有效的返回值：

<a href="" id="s-ok"></a>S \_ 正常  
已成功处理设备状态代码。 不会再调用错误处理程序。

如果出现错误状态代码 (模式对话框) ，这意味着会采取适当的措施来纠正错误，如 ADF 卡纸。

如果是信息状态代码，这只意味着向用户提供了一个无模式对话框，且不应将设备消息转发到行中的任何其他错误处理程序。

<a href="" id="wia-status-not-handled"></a>WIA \_ 状态 \_ 未 \_ 处理  
未采取任何措施向用户处理错误或报告状态。 如果将调用列表中的任何) ，则下一个处理程序 (。

这应该是错误处理程序的默认返回值。

<a href="" id="s-false"></a>S \_ FALSE  
用户取消了处理程序的无模式对话框的传输。 无论设备状态代码 (处理、未处理、错误或信息性) ，都可以在任何时候通过错误处理程序返回此返回值。

<a href="" id="other-error-codes"></a>其他错误代码  
如果无法从中恢复设备错误，或用户选择停止传输以响应显示的模式对话框，则错误处理程序应返回设备状态代码本身 (参阅 "示例" 部分) 中的示例。 当然，这意味着错误处理程序会处理设备状态代码。

此外，错误处理程序必须在处理设备状态代码时保持一致。 也就是说，错误处理程序的实例无法选择在时间 t0 处理状态代码 WIA \_ 状态 \_ xyz (或 WIA \_ 错误 \_ xyz) ，并决定不在时间 t1 进行处理。

以下代码是无效错误处理程序的示例：

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

删除 *HandleMessageNow* 例程会使此错误处理程序有效。

 

 




