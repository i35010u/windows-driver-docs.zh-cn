---
title: 支持扩展单元的自动更新事件
description: 支持扩展单元的自动更新事件
keywords:
- 自动更新事件 WDK USB 视频类
- 自动更新事件 WDK USB 视频类，扩展单元
- 事件 WDK USB 视频类
- 事件 WDK USB 视频类，随扩展单元自动更新
- 扩展单元-WDK USB 视频类，示例
- 示例代码 WDK USB 视频类、自动更新事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e28e27d7e4ec0a21450dc83557e52e6c4212e047
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809821"
---
# <a name="supporting-autoupdate-events-with-extension-units"></a>支持扩展单元的自动更新事件


本主题包含演示如何支持自动更新事件的示例代码。

在应用程序源中包含名为 TestApp 的以下代码：

```cpp
hEvent = CreateEvent(NULL, FALSE, FALSE, NULL);
if (!hEvent)
{
    printf("CreateEvent failed\n");
    goto errExit;
}
Event.Set = KSEVENTSETID_VIDCAPNotify;
Event.Id = KSEVENT_VIDCAP_AUTO_UPDATE;
Event.Flags = KSEVENT_TYPE_ENABLE;

EventData.NotificationType = KSEVENTF_EVENT_HANDLE;
EventData.EventHandle.Event = hEvent;
EventData.EventHandle.Reserved[0] = 0;
EventData.EventHandle.Reserved[1] = 0;

// register for autoupdate events
hr = m_pKsControl->KsEvent(
    &Event, 
 sizeof(KSEVENT), 
    &EventData, 
 sizeof(KSEVENTDATA), 
    &ulBytesReturned);
if (FAILED(hr))
{
    printf("Failed to register for auto-update event : %x\n", hr);
 goto errExit;
}

// Wait for event for 5 seconds 
dwError = WaitForSingleObject(hEvent, 5000);

// cancel further notifications
hr = m_pKsControl->KsEvent(
    NULL, 
    0, 
    &EventData, 
 sizeof(KSEVENTDATA), 
    &ulBytesReturned);
if (FAILED(hr))  printf("Cancel event returns : %x\n", hr);

if ((dwError == WAIT_FAILED) || 
   (dwError == WAIT_ABANDONED) ||
   (dwError == WAIT_TIMEOUT))
{
    printf("Wait failed : %d\n", dwError);
 goto errExit;
} 
printf("Wait returned : %d\n", dwError);

// handle the autoupdate event..
```

 

 




