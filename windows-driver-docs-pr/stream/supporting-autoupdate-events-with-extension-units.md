---
title: 支持扩展单元的自动更新事件
description: 支持扩展单元的自动更新事件
ms.assetid: 3dc75f48-adc7-4443-8090-2e61b3306798
keywords:
- 自动更新事件 WDK USB 视频类
- 自动更新事件 WDK USB 视频类扩展单位
- 事件 WDK USB 视频类
- 事件 WDK USB 视频类，与扩展单位的自动更新
- 扩展单位 WDK USB 视频类，示例
- 示例代码 WDK USB 视频类，自动更新事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 904f7662fe10907f6dc2e11a250abf3e7a48b2c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378516"
---
# <a name="supporting-autoupdate-events-with-extension-units"></a>支持扩展单元的自动更新事件


本主题包含演示如何支持自动更新事件的示例代码。

在应用程序源中，任意名为 TestApp.cpp 包括下面的代码：

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

 

 




