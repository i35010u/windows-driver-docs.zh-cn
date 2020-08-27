---
description: 支持事件 Cookie
title: 支持事件 Cookie
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5a83e6d0f41252d81d59a7002907cd2119bbae0
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969096"
---
# <a name="supporting-event-cookies"></a>支持事件 Cookie


当 WPD 应用程序调用 **IPortableDevice：： open** 方法或 **IPortableDeviceService：： open** 方法时，它们可以在客户端信息中指定一个唯一字符串或 "cookie"。 当这些应用程序向驱动程序注册其事件处理程序时，驱动程序会将此 cookie 与事件数据一起返回。 通过检查 cookie，应用程序可以确定是否应处理给定的事件。

例如，应用程序 A 在设备上创建一个对象，并接收 \_ \_ \_ 包含其客户端事件 cookie 的 WPD 事件对象添加事件。 由于在创建对象时已更新视图，因此应用程序 A 可以选择不刷新其设备内容的视图。 如果应用程序 B 在设备上创建了另一个对象，则应用程序 A 会接收 WPD \_ 事件 \_ 对象 \_ 添加的事件，该事件具有不同的 cookie (或没有 cookie) 。 通过检查 cookie，应用程序 A 可以采取相应的操作并刷新设备内容视图，因为应用程序 B 添加了新的对象。 由于 WPD 事件将广播到所有应用程序，因此当应用程序筛选出在以前与设备交互过程中触发的事件时，事件 cookie 最有用。

根据应用程序的不同，cookie 可能包含应用程序或 CLSID 的可执行文件名称，或者应用程序在可同时运行多个实例时创建的唯一标识符。 实际字符串内容对驱动程序并不重要。

在可以有两个或更多个客户端应用程序进行通信的环境中 (Windows 资源管理器实际上可以通过 WPD Shell 命名空间扩展) 一个客户端，因此最好支持事件 cookie 机制。 执行此操作是一种很好的 WPD 编程做法，可帮助将客户端流量降低到设备以响应事件并简化应用程序端事件处理。

## <a name="span-idsteps_to_support_the_event_cookiespanspan-idsteps_to_support_the_event_cookiespanspan-idsteps_to_support_the_event_cookiespansteps-to-support-the-event-cookie"></a><span id="Steps_to_Support_the_Event_Cookie"></span><span id="steps_to_support_the_event_cookie"></span><span id="STEPS_TO_SUPPORT_THE_EVENT_COOKIE"></span>支持事件 Cookie 的步骤


以下步骤标识了如何 \_ \_ \_ 在 WPD 驱动程序中支持 WPD 客户端事件 COOKIE：

1.  为 WPD \_ 命令 \_ COMMON \_ SAVE \_ CLIENT \_ INFORMATION 命令添加处理程序。 WDK 中的 WpdWudfSampleDriver 在 **WpdBaseDriver：： OnSaveClientInfo** 方法中包含此示例。
2.  在 **OnSaveClientInfo** 方法中，如果应用程序 \_ \_ \_ 在客户端信息参数中设置 WPD 客户端事件 COOKIE，请将该 cookie 与上下文信息一起保存。 某些应用程序可能会选择不发送此 cookie，在这种情况下，你的驱动程序在执行此步骤时不需要执行任何操作。
3.  发布事件时，如果客户端事件 cookie 可用，则将其与事件参数一起发送。 在示例驱动程序中，将在 **PostWpdEvent** 函数中添加此代码。

下面的代码示例演示了 WpdWudfSampleDriver 如何处理前面列表中的第二步。

```ManagedCPlusPlus
LPWSTR pszEventCookie = NULL; 
hr = pClientInfo->GetStringValue(WPD_CLIENT_EVENT_COOKIE, &pszEventCookie);
if (hr == S_OK && pszEventCookie != NULL){    
// Store the cookie value with the client context    
pContext->EventCookie = pszEventCookie;
}
CoTaskMemFree(pszEventCookie);
```

下面的代码示例演示了 WpdWudfSampleDriver 如何处理前面列表中的第三步。

```ManagedCPlusPlus
HRESULT hrEventCookie = GetClientEventCookie(pCommandParams, &pszEventCookie);
if (hrEventCookie == S_OK && pszEventCookie != NULL)
{    
// Add it to the event parameters    
// The application's OnEvent callback will match this with its cookie    
hrEventCookie = pEventParams->SetStringValue(WPD_CLIENT_EVENT_COOKIE, pszEventCookie);
}
CoTaskMemFree(pszEventCookie);
```

下面的代码示例包含 GetClientEventCookie helper 函数的大纲。 Helper 函数使用在命令参数中提供的客户端信息上下文在上下文映射中查找保存的客户端 cookie。

```ManagedCPlusPlus
ClientContext* pClientContext = NULL;   
// This is a context helper object defined by the sample 
driverhr = pCommandParams->GetStringValue(WPD_PROPERTY_COMMON_CLIENT_INFORMATION_CONTEXT, &pszClientContext);
if (hr == S_OK)
{    
hr = GetClientContext(pCommandParams, pszClientContext, (IUnknown**)&pClientContext);    
if (hr == S_OK && pClientContext != NULL && pClientContext->EventCookie.GetLength() > 0)    
{       
// Allocate the cookie string to return        
*ppszEventCookie = AtlAllocTaskWideString(pClientContext->EventCookie);    
}    
if (pClientContext != NULL)          
pClientContext->Release();    
CoTaskMemFree(pszClientContext);
}
```

 

 




