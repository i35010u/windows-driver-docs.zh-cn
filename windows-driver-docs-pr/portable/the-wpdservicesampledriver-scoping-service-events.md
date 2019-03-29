---
Description: Scoping Service Events
title: 限定服务事件的范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 048b2a54edc0fd92f504c1d31b0c8290d0a0acbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576050"
---
# <a name="scoping-service-events"></a>限定服务事件的范围


默认情况下，WPD 广播到所有客户端应用程序 （甚至的客户端连接到其他服务） 的服务事件。 若要限制的广播范围，驱动程序必须设置 WPD\_对象\_容器\_功能\_对象\_ID 事件参数应为其广播的服务的 ObjectID有限。

下面的代码示例演示如何**WPD\_对象\_容器\_功能\_位于\_ID**添加到中的事件参数**FakeDevice::SetPropertyValues**，以指示已更新对象：

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

联系人服务内的对象*pContent-&gt;ContainerFunctionalObjectID*包含联系人服务的对象标识符。 如果指定此参数，则 WPD 匹配此事件参数和筛选事件，以便连接到同一个联系人服务其他客户端将会收到此事件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





