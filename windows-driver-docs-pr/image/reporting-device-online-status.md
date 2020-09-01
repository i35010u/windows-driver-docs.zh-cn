---
title: 报告设备联机状态
description: 报告设备联机状态
ms.assetid: 59ce747a-bb5e-4e8c-ab4a-d3f4432f17e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6dba638576bb849ee1027b161dc1dd1752e98e3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188890"
---
# <a name="reporting-device-online-status"></a>报告设备联机状态





WIA 服务通过调用 [**IStiUSD：： GetStatus**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus) 方法来检查 WIA 设备的联机状态。 WIA 微型驱动程序应检查硬件的当前联机状态并报告结果。

WIA 服务调用 **IStiUSD：： GetStatus** 方法执行两个主要操作：

-   检查设备的联机状态。

-   轮询设备事件，例如推送按钮事件。

可以通过检查[**STI \_ 设备 \_ 状态**](/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status)结构的**StatusMask**成员来确定操作请求。 **StatusMask**成员可以是以下请求之一。

<a href="" id="sti-devstatus-online-state"></a>STI \_ DEVSTATUS \_ ONLINE \_ 状态  
检查设备是否处于联机状态。

<a href="" id="sti-devstatus-events-state"></a>STI \_ DEVSTATUS \_ 事件 \_ 状态  
检查设备事件。

### <a name="sti_devstatus_online_state"></a><a href="" id="sti-devstatus-online-state"></a>STI \_ DEVSTATUS \_ ONLINE \_ 状态

此操作请求应通过设置 STI **dwOnlineState** \_ 设备状态结构的 dwOnlineState 成员执行 \_ 。

### <a name="sti_devstatus_events_state"></a><a href="" id="sti-devstatus-events-state"></a>STI \_ DEVSTATUS \_ 事件 \_ 状态

此操作请求应通过设置 STI **dwEventHandlingState** \_ 设备状态结构的 dwEventHandlingState 成员执行 \_ 。 应使用的值为 STI \_ EVENTHANDLING \_ PENDING。  (设备有一个挂起的事件，并等待向 WIA 服务报告该事件。 ) 

设置 STI \_ EVENTHANDLING \_ PENDING 后，wia 服务将收到有关 wia 驱动程序中发生的事件的信号。 WIA 服务调用 [**IStiUSD：： GetNotificationData**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata) 方法来获取有关事件的详细信息。

对于轮询事件和中断事件，将调用 **IStiUSD：： GetNotificationData** 方法。 在此方法中，你应填写适当的事件信息以返回到 WIA 服务。

**注意**   \_ \_ 请始终在**dwEventHandlingState**成员中清除 STI EVENTHANDLING 挂标志，以确保在发生设备事件时正确设置该标志。

 

下面的示例演示 **IStiUSD：： GetStatus** 方法的实现。

```cpp
STDMETHODIMP CWIADevice::GetStatus(PSTI_DEVICE_STATUS pDevStatus)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if(!pDevStatus)
  {
      return E_INVALIDARG;
  }

  HRESULT hr = S_OK;

  //
  // If we are asked, verify the device is online.
  //

  if (pDevStatus->StatusMask & STI_DEVSTATUS_ONLINE_STATE) {

    //
    // assume the device is OFF-LINE before continuing. This will
    // validate that the online check was successful.
    //

    pDevStatus->dwOnlineState = STI_ONLINESTATE_OFFLINE;

    if(MyDeviceIsOnlineStatus()) {
 
      //
      // device is ON-LINE and operational
      //

      pDevStatus->dwOnlineState |= STI_ONLINESTATE_OPERATIONAL;
    } else {

      //
      // device is OFF-LINE and NOT operational
      //

 }
  }
  return S_OK;
}
```

 

