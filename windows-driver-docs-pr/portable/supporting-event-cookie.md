---
Description: 支持事件 Cookie
title: 支持事件 Cookie
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61ebf90a6099af34ff0c7eca57c2f5fb777f5d64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380851"
---
# <a name="supporting-event-cookies"></a>支持事件 Cookie


WPD 应用程序可以指定唯一的字符串或"cookie"中的客户端信息时调用它们**IPortableDevice::Open**方法或**IPortableDeviceService::Open**方法。 使用驱动程序，这些应用程序注册其事件处理程序，驱动程序将返回此 cookie，其事件数据。 通过检查 cookie，应用程序可以确定是否应处理给定的事件。

例如，应用程序 A 在设备上创建一个对象，并接收 WPD\_事件\_对象\_已添加事件，其中包含其客户端事件 cookie。 应用程序 A 可以选择不刷新其设备内容的视图，因为在创建对象时的时间更新视图。 如果应用程序 B 在设备上创建另一个对象，应用程序 A 接收 WPD\_事件\_对象\_ADDED 事件具有不同的 cookie （或任何 cookie）。 通过检查 cookie，应用程序的可能需要相应的操作和查看设备的内容，请刷新，因为应用程序 B 添加新的对象。 WPD 事件会广播到所有应用程序，因为事件 cookie 是最有用，当应用程序筛选出它必须在与设备交互的上一个过程中触发的事件。

根据应用程序，该 cookie 可能包含应用程序或 CLSID 或如果它可以同时运行多个实例创建的应用程序的唯一标识符的可执行文件名称。 向驱动程序时，实际的字符串内容确实很重要。

在环境中可以有两个或更多客户端应用程序通信与驱动程序 （几乎保证 Windows 资源管理器是一台客户端通过 WPD Shell Namespace 扩展），它是支持事件 cookie 机制的一个好办法。 执行此操作是一个好的 WPD 编程做法，可帮助减少客户端流量到你的设备以响应事件和简化应用程序端事件处理。

## <a name="span-idstepstosupporttheeventcookiespanspan-idstepstosupporttheeventcookiespanspan-idstepstosupporttheeventcookiespansteps-to-support-the-event-cookie"></a><span id="Steps_to_Support_the_Event_Cookie"></span><span id="steps_to_support_the_event_cookie"></span><span id="STEPS_TO_SUPPORT_THE_EVENT_COOKIE"></span>支持事件 Cookie 的步骤


以下步骤确定如何支持 WPD\_客户端\_事件\_WPD 驱动程序中的 COOKIE:

1.  添加的处理程序 WPD\_命令\_常见\_保存\_客户端\_信息命令。 从 WDK WpdWudfSampleDriver 包含出现在这种**WpdBaseDriver::OnSaveClientInfo**方法。
2.  在中**OnSaveClientInfo**方法时，如果应用程序设置 WPD\_客户端\_事件\_COOKIE 在客户端信息参数中，将 cookie 保存到与你的上下文信息。 某些应用程序可能选择不发送此 cookie，这种情况下您的驱动程序无需执行任何操作此步骤。
3.  当在发布事件，如果客户端事件 cookie 可用时，将其发送以及事件参数。 在示例驱动程序，此代码将添加到**PostWpdEvent**函数。

下面的代码示例演示如何 WpdWudfSampleDriver 句柄： 逐步了解上述列表中的两个。

```ManagedCPlusPlus
LPWSTR pszEventCookie = NULL; 
hr = pClientInfo->GetStringValue(WPD_CLIENT_EVENT_COOKIE, &pszEventCookie);
if (hr == S_OK && pszEventCookie != NULL){    
// Store the cookie value with the client context    
pContext->EventCookie = pszEventCookie;
}
CoTaskMemFree(pszEventCookie);
```

下面的代码示例演示如何 WpdWudfSampleDriver 句柄： 逐步了解上述列表中的三个。

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

下面的代码示例包含 GetClientEventCookie 帮助程序函数的概述。 帮助程序函数使用要查找已保存的客户端 cookie 上下文映射中的命令参数中提供的客户端的信息上下文。

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

 

 




