---
title: 添加轮询事件支持
description: 添加轮询事件支持
ms.assetid: 7c7617d4-22d6-48a8-b69c-dd0347f078dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48b385f5f99b356e4906fd04dbda0373ffa50871
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192105"
---
# <a name="adding-polling-event-support"></a>添加轮询事件支持





若要正确设置 WIA 驱动程序以报告轮询事件，请执行以下操作：

1.  设置设备 INF 文件中的 **功能 = 0x33** 。 有关详细信息，请参阅用于 [WIA 设备的 INF 文件](inf-files-for-wia-devices.md) (。 ) 

2.  在 \_ \_ \_ \_ \_ \_ [**PUSHSUPPORT：： IStiUSD**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities) 方法中报表 STI GENCAP 通知和 STI USD GENCAP NATIVE GetCapabilities。

3.  报告 [**IWiaMiniDrv：:D rvgetcapabilities**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities) 方法中所有受支持的事件。

4.  响应对 [**IStiUSD：： GetStatus**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus) 方法的调用。 WIA 服务按在 INF 文件中可配置的预设间隔调用此方法。 默认设置为1秒的间隔。

5.  在 [**IStiUSD：： GetNotificationData**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata) 方法中报告正确的事件信息响应。

WIA 服务调用 **IStiUSD：： GetStatus** 方法执行两个主要操作：

1.  检查设备的联机状态。

2.  轮询设备事件，例如推送按钮事件。

可以通过检查[**STI \_ 设备 \_ 状态**](/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status)结构的**StatusMask**成员来确定操作请求。 **StatusMask**成员可以是以下请求之一：

<a href="" id="sti-devstatus-online-state"></a>STI \_ DEVSTATUS \_ ONLINE \_ 状态  
此操作请求检查设备是否处于联机状态，是否应通过设置 STI **dwOnlinesState** \_ 设备状态结构的 dwOnlinesState 成员来填充设备 \_ 。

<a href="" id="sti-devstatus-events-state"></a>STI \_ DEVSTATUS \_ 事件 \_ 状态  
此操作请求检查设备事件。 应通过设置 STI **dwEventHandlingState** \_ 设备状态结构的 dwEventHandlingState 成员来填充它 \_ 。 应使用的值为 STI \_ EVENTHANDLING \_ PENDING。  (设备有一个挂起的事件，并等待向 WIA 服务报告该事件。 ) 

设置 STI \_ EVENTHANDLING \_ PENDING 后，wia 服务将收到有关 wia 驱动程序中发生的事件的信号。 WIA 服务调用 **IStiUSD：： GetNotificationData** 方法来获取有关事件的详细信息。

对于轮询事件和中断事件，将调用 **IStiUSD：： GetNotificationData** 方法。 在此方法中，你应填写适当的事件信息以返回到 WIA 服务。

**注意**   \_ \_ 请始终在**dwEventHandlingState**成员中清除 STI EVENTHANDLING 挂标志，以确保在发生设备事件时正确设置该标志。
检测到事件时，此 WIA 驱动程序应将 *m \_ guidLastEvent* 类成员变量设置为正确的事件 GUID。 当 WIA 服务调用**IStiUSD：： GetNotificationData**方法时，将检查*m \_ guidLastEvent* 。 在**CWIADevice**类中定义*m \_ guidLastEvent*成员变量 (在以下代码段) 中，用于缓存最后一个发出信号的事件。 WIA 服务请求此成员变量后，它始终设置为 GUID \_ NULL。

 

下面的示例演示 [**IStiUSD：： GetStatus**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus) 方法的实现。

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

 

