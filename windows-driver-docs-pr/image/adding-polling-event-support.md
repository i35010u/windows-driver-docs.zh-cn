---
title: 添加轮询事件支持
description: 添加轮询事件支持
ms.assetid: 7c7617d4-22d6-48a8-b69c-dd0347f078dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d8b29e300f68146ad7daee89cff4eeb37094915
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542081"
---
# <a name="adding-polling-event-support"></a>添加轮询事件支持





若要正确设置您 WIA 的驱动程序报告轮询事件，请执行以下操作：

1.  设置**功能 = 0x33**设备的 INF 文件中。 (请参阅[WIA 设备 INF 文件](inf-files-for-wia-devices.md)有关详细信息。)

2.  报告 STI\_GENCAP\_通知和 STI\_美元\_GENCAP\_本机\_PUSHSUPPORT 中的[ **IStiUSD::GetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543817)方法。

3.  中的所有报表支持事件[ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)方法。

4.  响应对的调用[ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823)方法。 WIA 服务调用此方法在预设的间隔的 INF 文件中进行配置。 默认设置为 1 秒时间间隔。

5.  报告中的相应的事件信息响应[ **IStiUSD::GetNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543821)方法。

WIA 服务调用**IStiUSD::GetStatus**针对两个主要操作的方法：

1.  正在检查设备的联机状态。

2.  轮询设备事件，例如已下压按钮的事件。

确定操作请求可以通过检查**StatusMask**的成员[ **STI\_设备\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff548369)结构。 **StatusMask**成员可以是以下请求：

<a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_ONLINE\_状态  
此操作请求检查设备是否处于联机状态，并且应设置来填充**dwOnlinesState** STI 成员\_设备\_状态结构。

<a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_事件\_状态  
此操作请求检查设备事件。 它应通过设置填充**dwEventHandlingState** STI 成员\_设备\_状态结构。 应使用的值是 STI\_EVENTHANDLING\_PENDING。 （该设备具有挂起的事件并且正在等待其报告给 WIA 服务）

当 STI\_EVENTHANDLING\_设置 PENDING、 WIA 服务发出信号事件发生 WIA 驱动程序中。 WIA 服务调用**IStiUSD::GetNotificationData**方法以获取有关事件的详细信息。

**IStiUSD::GetNotificationData**轮询的事件和中断事件的调用方法。 它是在此方法中，您应填写相应的事件信息以返回到 WIA 服务。

**请注意**  * * * 始终清除 STI\_EVENTHANDLING\_挂起中标志**dwEventHandlingState**成员以确保它正确设置设备事件发生时。
此 WIA 驱动程序应设置*m\_guidLastEvent*到相应的事件 GUID 时检测到事件的类成员变量。 *M\_guidLastEvent* WIA 的服务的调用时更高版本同时选中**IStiUSD::GetNotificationData**方法。 *M\_guidLastEvent*中定义成员变量**CWIADevice**类 （在下面的代码段），用于缓存的最后一个事件发出信号。 此成员变量已 WIA 服务请求后，始终设置为 GUID\_NULL。

 

下面的示例演示的实现[ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823)方法。

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
  // If we are asked, verify state of an event handler 
  //(front panel buttons, user controlled attachments, etc.).
  //
  // If your device requires polling, then this is where you would
  // specify the event result.
  // However, It is not recommended to have polled events.
  // Interrupt events are better for performance, and reliability.
  // See the SetNotificationsHandle method for how to
  // implement interrupt events.
  //

  //
  // clear the dwEventHandlingState field first to make sure we are really setting
  // a pending event.
  //

  pDevStatus->dwEventHandlingState &= ~STI_EVENTHANDLING_PENDING;
  if (pDevStatus->StatusMask & STI_DEVSTATUS_EVENTS_STATE) {

    //
    // set the polled event result here, for the GetNotificationData()
    // method to read and report.
    // (m_guidLastEvent will be read in GetNotificationData)
    //

    LONG lEventResult = 0;
    PollMyDeviceForEvents(&lEventResult)

    if(lEventResult == DEVICE_SCAN_BUTTON_PRESSED) {

        //
        // polled event result was one we know about
        //

        m_guidLastEvent = WIA_EVENT_SCAN_IMAGE;
    } else {

        //
        // nothing happened, so continue
        //

        m_guidLastEvent = GUID_NULL;
    }

    if (m_guidLastEvent != GUID_NULL) {

        //
        // if the event GUID is NOT GUID_NULL, set the
        // STI_EVENTHANDLING_PENDING flag letting the WIA service
        // know that we have an event ready. This will tell the WIA
        // service to call GetNotificationData() for the event
        // specific information.
        //

        pDevStatus->dwEventHandlingState |= STI_EVENTHANDLING_PENDING;
    }
  }
  return S_OK;
}
```

 

 




