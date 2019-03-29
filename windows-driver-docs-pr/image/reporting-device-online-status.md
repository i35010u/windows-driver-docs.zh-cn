---
title: 报告设备联机状态
description: 报告设备联机状态
ms.assetid: 59ce747a-bb5e-4e8c-ab4a-d3f4432f17e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 214f4fc6fdf73cb1eddb8c9fda3c6c3c1b217c5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567122"
---
# <a name="reporting-device-online-status"></a>报告设备联机状态





WIA 服务检查 WIA 设备的联机状态，通过调用[ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823)方法。 WIA 微型驱动程序应检查硬件的当前联机状态，并报告结果。

WIA 服务调用**IStiUSD::GetStatus**针对两个主要操作的方法：

-   正在检查设备的联机状态。

-   轮询设备事件，例如已下压按钮的事件。

确定操作请求可以通过检查**StatusMask**的成员[ **STI\_设备\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff548369)结构。 **StatusMask**成员可以是以下请求。

<a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_ONLINE\_状态  
检查设备是否处于联机状态。

<a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_事件\_状态  
检查设备事件。

### <a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_ONLINE\_状态

此操作请求应执行通过设置**dwOnlineState** STI 成员\_设备\_状态结构。

### <a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_事件\_状态

此操作请求应执行通过设置**dwEventHandlingState** STI 成员\_设备\_状态结构。 应使用的值是 STI\_EVENTHANDLING\_PENDING。 （该设备具有挂起的事件并且正在等待其报告给 WIA 服务）

当 STI\_EVENTHANDLING\_设置 PENDING、 WIA 服务发出信号事件发生 WIA 驱动程序中。 WIA 服务调用[ **IStiUSD::GetNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543821)方法以获取有关事件的详细信息。

**IStiUSD::GetNotificationData**轮询的事件和中断事件的调用方法。 它是在此方法中，您应填写相应的事件信息以返回到 WIA 服务。

**请注意**  始终清除 STI\_EVENTHANDLING\_挂起中标志**dwEventHandlingState**成员以确保它正确设置设备事件发生时。

 

下面的示例演示的实现**IStiUSD::GetStatus**方法。

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

 

 




