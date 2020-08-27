---
description: 限定服务事件的范围
title: 限定服务事件的范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfa5f8eebc0a6fe41d49e40a561f0db50ca70dd4
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969574"
---
# <a name="scoping-service-events"></a>限定服务事件的范围


默认情况下，WPD 会将服务事件广播到所有客户端应用程序， (甚至是连接到其他服务) 的客户端。 若要限制广播的作用域，驱动程序必须将 WPD \_ 对象 \_ 容器 \_ 功能 \_ 对象 \_ ID 事件参数设置为广播应受限到的服务的 ObjectID。

下面的代码示例演示如何将 **WPD \_ 对象 \_ 容器 \_ 功能 \_ OBEJCT \_ ID** 添加到 **FakeDevice：： SetPropertyValues**中的事件参数，以指示对象已更新：

```ManagedCPlusPlus
        if (SUCCEEDED(hr) && (*pbObjectChanged)) 
        {
            HRESULT hrEvent = pEventParams->SetGuidValue(WPD_EVENT_PARAMETER_EVENT_ID, WPD_EVENT_OBJECT_UPDATED);
            CHECK_HR(hrEvent, "Failed to add WPD_EVENT_PARAMETER_EVENT_ID");

        . . .

            if (hrEvent == S_OK)
            {
                // Adding this event parameter will allow WPD to scope this event to the container functional object
                hrEvent = pEventParams->SetStringValue(WPD_OBJECT_CONTAINER_FUNCTIONAL_OBJECT_ID, pContent->ContainerFunctionalObjectID);
                CHECK_HR(hrEvent, "Failed to add WPD_OBJECT_CONTAINER_FUNCTIONAL_OBJECT_ID");
            }
        }
```

对于联系人服务中的对象， *pContent- &gt; ContainerFunctionalObjectID* 包含联系人服务的对象标识符。 如果指定此参数，WPD 将与此事件参数匹配并筛选事件，以便仅连接到同一联系人服务的其他客户端将收到此事件。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





