---
title: 报告设备联机状态
description: 报告设备联机状态
ms.assetid: 59ce747a-bb5e-4e8c-ab4a-d3f4432f17e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 377bb769a4a036f36c5b92bc7d93d3ece8b9835b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840755"
---
# <a name="reporting-device-online-status"></a>报告设备联机状态





WIA 服务通过调用[**IStiUSD：： GetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)方法来检查 WIA 设备的联机状态。 WIA 微型驱动程序应检查硬件的当前联机状态并报告结果。

WIA 服务调用**IStiUSD：： GetStatus**方法执行两个主要操作：

-   检查设备的联机状态。

-   轮询设备事件，例如推送按钮事件。

若要确定操作请求，可以通过检查[**STI\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status)的**STATUSMASK**成员\_状态结构来完成。 **StatusMask**成员可以是以下请求之一。

<a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_联机\_状态  
检查设备是否处于联机状态。

<a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_事件\_状态  
检查设备事件。

### <a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_联机\_状态

此操作请求应通过将 STI\_设备的**dwOnlineState**成员设置\_状态结构来执行。

### <a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_事件\_状态

此操作请求应通过将 STI\_设备的**dwEventHandlingState**成员设置\_状态结构来执行。 应使用的值是 STI\_EVENTHANDLING\_挂起的。 （设备的事件处于挂起状态，正在等待向 WIA 服务报告该事件。）

设置 STI\_EVENTHANDLING\_"挂起" 时，WIA 服务将收到 WIA 驱动程序中发生的事件的信号。 WIA 服务调用[**IStiUSD：： GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)方法来获取有关事件的详细信息。

对于轮询事件和中断事件，将调用**IStiUSD：： GetNotificationData**方法。 在此方法中，你应填写适当的事件信息以返回到 WIA 服务。

**请注意**   始终清除**dwEventHandlingState**成员中的 STI\_EVENTHANDLING\_挂起标志，以确保在发生设备事件时正确设置该标志。

 

下面的示例演示**IStiUSD：： GetStatus**方法的实现。

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

 

 




