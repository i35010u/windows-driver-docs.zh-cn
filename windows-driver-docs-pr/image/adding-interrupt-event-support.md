---
title: 添加中断事件支持
description: 添加中断事件支持
ms.assetid: 74fbaa7c-f058-4b17-b278-3dea0faf4431
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 889e70793d24db6e8472787e231852f23179bacd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383398"
---
# <a name="adding-interrupt-event-support"></a>添加中断事件支持





若要正确设置 WIA 驱动程序来报告中断事件，请执行以下操作：

1.  设置**功能 = 0x31**设备的 INF 文件中。 (请参阅[WIA 设备 INF 文件](inf-files-for-wia-devices.md)有关详细信息。)

2.  报告 STI\_GENCAP\_通知和 STI\_美元\_GENCAP\_本机\_PUSHSUPPORT 中的[ **IStiUSD::GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getcapabilities)方法。

3.  中的所有报表支持事件[ **IWiaMiniDrv::drvGetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法。

4.  缓存和使用中传递的事件句柄[ **IStiUSD::SetNotificationHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-setnotificationhandle)方法。 这是设备信号的事件句柄或 WIA 微型驱动程序发出信号直接使用**SetEvent** （Microsoft Windows SDK 文档中所述）。 它在这种方法是，启动 WIA 设备的等待状态。

5.  报告中的相应的事件信息响应[ **IStiUSD::GetNotificationData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getnotificationdata)方法。

以下两个示例演示使用的实现配置你的设备进行中断**IWiaMiniDrv::drvGetCapabilities**并**IStiUSD::SetNotificationHandle**方法。

**请注意**  务必使用重叠的 I/O 调用包含涉及内核模式驱动程序的所有活动。 这允许适当的超时和设备请求取消。

 

### <a href="" id="explanation-of-the-iwiaminidrv-drvgetcapabilities-implementation"></a>IWiaMiniDrv::drvGetCapabilities 实现的说明

WIA 服务调用**IWiaMiniDrv::drvGetCapabilities**方法来获取 WIA 设备支持事件和命令。 WIA 驱动程序应首先看一下传入*lFlags*参数，以确定该请求应回答。

WIA 驱动程序应分配内存 （以将 WIA 驱动程序使用的并由其释放） 使其包含的数组[ **WIA\_DEV\_CAP\_DRV** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_dev_cap_drv)结构。 在调用**IWiaMiniDrv::drvGetCapabilities**，将指针传递到存储中的 WIA 驱动程序分配内存的地址的内存位置*ppCapabilities*参数。

**请注意**   WIA 服务不会释放此内存。 请务必 WIA 驱动程序管理的已分配的内存。

 

下面的示例演示的实现[ **IWiaMiniDrv::drvGetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法。

```cpp
HRESULT _stdcall CWIADevice::drvGetCapabilities(
  BYTE            *pWiasContext,
  LONG            lFlags,
  LONG            *pcelt,
  WIA_DEV_CAP_DRV **ppCapabilities,
  LONG            *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
  //  then fail the call and return E_INVALIDARG.
  //

  if (!pWiasContext) {

    //
    // The WIA service may pass in a NULL for the pWiasContext. 
    // This is expected because there is a case where no item 
    // was created at the time the event was fired.
    //
  }

  if (!plDevErrVal) {
      return E_INVALIDARG;
  }

  if (!pcelt) {
      return E_INVALIDARG;
  }

  if (!ppCapabilities) {
      return E_INVALIDARG;
  }

  *plDevErrVal = 0;

  HRESULT hr = S_OK;

  LONG lNumberOfCommands = 1;
  LONG lNumberOfEvents   = 2;

  //
  // initialize WIA driver capabilities ARRAY
  // a member WIA_DEV_CAP_DRV m_Capabilities[3] variable
  // This memory should live with the WIA minidriver.
  // A pointer to this structure is given to the WIA service using
  // ppCapabilities.  Do not delete this memory until
  // the WIA minidriver has been unloaded.
  //

  // This ARRAY should only be initialized once.
  // The Descriptions and Names should be read from the proper
  // string resource.  These string values should be localized in
  // multiple languages because an application will be use them to
  // be displayed to the user.
  //

  // Command #1
  m_Capabilities[0].wszDescription =   L"Synchronize Command";
  m_Capabilities[0].wszName = L"Synchronize";
  m_Capabilities[0].guid    = (GUID*)&WIA_CMD_SYNCHRONIZE;
  m_Capabilities[0].lFlags = 0;
  m_Capabilities[0].wszIcon = WIA_ICON_SYNCHRONIZE;

  // Event #1
  m_Capabilities[1].wszDescription = L"Scan Button";
  m_Capabilities[1].wszName = L"Scan";
  m_Capabilities[1].guid    = (GUID*)&WIA_EVENT_SCAN_IMAGE;
  m_Capabilities[1].lFlags = WIA_NOTIFICATION_EVENT | WIA_ACTION_EVENT;
  m_Capabilities[1].wszIcon = WIA_ICON_SCAN_BUTTON_PRESS;

  // Event #2
  m_Capabilities[2].wszDescription = L"Copy Button";
  m_Capabilities[2].wszName = L"Copy";
  m_Capabilities[2].guid    = (GUID*)&WIA_EVENT_SCAN_PRINT_IMAGE;
  m_Capabilities[2].lFlags = WIA_NOTIFICATION_EVENT | WIA_ACTION_EVENT;
  m_Capabilities[2].wszIcon = WIA_ICON_SCAN_BUTTON_PRESS;


  //
  //  Return depends on flags.  Flags specify whether we should return
  //  commands, events, or both.
  //
  //

  switch (lFlags) {
  case WIA_DEVICE_COMMANDS:

    //
    //  report commands only
    //

    *pcelt          = lNumberOfCommands;
    *ppCapabilities = &m_Capabilities[0];
    break;
  case WIA_DEVICE_EVENTS:

    //
    //  report events only
    //

    *pcelt          = lNumberOfEvents;
    *ppCapabilities = &m_Capabilities[1]; // start at the first event in the ARRAY
    break;
  case (WIA_DEVICE_COMMANDS | WIA_DEVICE_EVENTS):

    //
    //  report both events and commands
    //

     *pcelt          = (lNumberOfCommands + lNumberOfEvents);
     *ppCapabilities = &m_Capabilities[0];
     break;
  default:

    //
    //  invalid request
    //
    hr = E_INVALIDARG;
    break;
  }

  return hr;
}
```

[ **IStiUSD::SetNotificationHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-setnotificationhandle) WIA 服务或在内部启动或停止事件通知此驱动程序调用方法。 WIA 服务将在创建使用有效句柄中传递**CreateEvent** （Microsoft Windows SDK 文档中介绍），指示 WIA 驱动程序在硬件中发生事件时通知此句柄。

**NULL**可以传递给**IStiUSD::SetNotificationHandle**方法。 **NULL**指示 WIA 微型驱动程序将停止设备的所有活动，并退出任何事件的等待操作。

下面的示例演示的实现**IStiUSD::SetNotificationHandle**方法。

```cpp
STDMETHODIMP CWIADevice::SetNotificationHandle(HANDLE hEvent)
{
  HRESULT hr = S_OK;

  if (hEvent && (hEvent != INVALID_HANDLE_VALUE)) {

    //
    // A valid handle indicates that we are asked to start our "wait"
    // for device interrupt events
    //

    //
    // reset last event GUID to GUID_NULL
    //

    m_guidLastEvent = GUID_NULL;

    //
    // clear EventOverlapped structure
    //

    memset(&m_EventOverlapped,0,sizeof(m_EventOverlapped));

    //
    // fill overlapped hEvent member with the event passed in by 
    // the WIA service. This handle will be automatically signaled
    //  when an event is triggered at the hardware level.
    //

    m_EventOverlapped.hEvent = hEvent;

    //
    // clear event data buffer.  This is the buffer that will be used
    //  to determine what event was signaled from the device.
    //

    memset(m_EventData,0,sizeof(m_EventData));

    //
    // use the following call for interrupt events on your device
    //

    DWORD dwError = 0;
    BOOL bResult = DeviceIoControl( m_hDeviceDataHandle,
                                    IOCTL_WAIT_ON_DEVICE_EVENT,
                                    NULL,
                                    0,
                                    &m_EventData,
                                    sizeof(m_EventData),
                                    &dwError,
                                    &m_EventOverlapped );

    if (bResult) {
        hr = S_OK;
    } else {
        hr = HRESULT_FROM_WIN32(::GetLastError());
    }

  } else {

    //
    // stop any hardware waiting events here, the WIA service has
    // notified us to stop all hardware event waiting
    //

    //
    // Stop hardware interrupt events. This will stop all activity on
    // the device. Since DeviceIOControl was used with OVERLAPPED i/o 
    // functionality the CancelIo() can be used to stop all kernel
    // mode activity.
    //


    if(m_hDeviceDataHandle){
        if(!CancelIo(m_hDeviceDataHandle)){

            //
            // canceling of the IO failed, call GetLastError() here to determine the cause.
            //

            LONG lError = ::GetLastError();

        }
    }
  }
  return hr;
}
```

当 WIA 微型驱动程序或 WIA 设备已检测到并发出信号事件时，WIA 服务调用[ **IStiUSD::GetNotificationData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getnotificationdata)方法。 它是事件的在此方法中 WIA 微型驱动程序应报告发生的详细信息。

WIA 服务调用**IStiUSD::GetNotificationData**方法以获取有关刚发送信号的事件信息。 **IStiUSD::GetNotificationData**可以作为两个事件操作的其中一个的结果调用方法。

1.  **IStiUSD::GetStatus**报告通过设置 STI 是否存在挂起的事件\_EVENTHANDLING\_挂起中标志[ **STI\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/ns-sti-_sti_device_status)结构。

2.  *HEvent*句柄由传入**IStiUSD::SetNotificationHandle**硬件，或通过调用收到信号**SetEvent** （Microsoft Windows SDK 中所述文档）。

WIA 驱动程序负责填写[ **STINOTIFY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/ns-sti-_stinotify)结构

下面的示例演示的实现**IStiUSD::GetNotificationData**方法。

```cpp
STDMETHODIMP CWIADevice::GetNotificationData( LPSTINOTIFY pBuffer )
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if(!pBuffer){
      return E_INVALIDARG;
  }
 
  GUID guidEvent = GUID_NULL;
  DWORD dwBytesRet = 0;
  BOOL bResult = GetOverlappedResult(m_hDeviceDataHandle, &m_EventOverlapped, &dwBytesRet, FALSE );
  if (bResult) {
    //
    // read the m_EventData buffer to determine the proper event.
    // set guidEvent to the proper event GUID
    // set guidEvent to GUID_NULL when an event has
    // not happened that you are concerned with
    //

    if(m_EventData[0] == DEVICE_SCAN_BUTTON_PRESSED) {
       guidEvent = WIA_EVENT_SCAN_IMAGE;
    } else {
       guidEvent = GUID_NULL;
    }
  }

  //
  // If the event was triggered, then fill in the STINOTIFY structure
  // with the proper event information
  //

  if (guidEvent != GUID_NULL) {
    memset(pBuffer,0,sizeof(STINOTIFY));
    pBuffer->dwSize               = sizeof(STINOTIFY);
    pBuffer->guidNotificationCode = guidEvent;        
  } else {
    return STIERR_NOEVENTS;
  }

  return S_OK;
}
```

中断事件可以随时停止通过传递**NULL**作为事件句柄。 微型驱动程序应将此视为信号停止硬件设备上的任何等待状态。

**请注意**   [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法可以接收影响事件等待状态的电源管理事件。

 

WIA 服务调用**IWiaMiniDrv::drvNotifyPnpEvent**方法，并将 WIA\_事件\_POWER\_系统即将置于睡眠状态时的挂起事件。 发生此调用时，设备可能已是从其等待状态。 睡眠状态会自动触发内核模式驱动程序退出任何等待状态，以允许系统进入此关闭的状态。 当系统从睡眠状态恢复时，WIA 服务将发送 WIA\_事件\_电源\_恢复事件。 这次 WIA 微型驱动程序必须重新建立中断事件等待状态。 有关睡眠状态的详细信息，请参阅[系统的电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-states)并[设备的电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)。

建议的 WIA 微型驱动程序缓存的事件句柄最初传递到[ **IStiUSD::SetNotificationHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-setnotificationhandle)方法，以便可以重复使用它，系统从睡眠状态唤醒时或休眠状态。

WIA 服务*却不*调用**IStiUSD::SetNotificationHandle**后系统已恢复的方法。 建议微型驱动程序调用其**IStiUSD::SetNotificationHandle**方法，并传递缓存的事件句柄。

WIA 服务调用**IWiaMiniDrv::drvNotifyPnpEvent**系统事件发生时的方法。 WIA 驱动程序应检查*pEventGUID*参数，以确定正在处理的事件。

必须处理一些常见事件是：

<a href="" id="wia-event-power-suspend"></a>WIA\_事件\_电源\_挂起  
系统正在进入挂起/睡眠模式。

<a href="" id="wia-event-power-resume"></a>WIA\_事件\_电源\_恢复  
系统从挂起/睡眠模式唤醒。

WIA 驱动程序应返回从挂起后进行还原的任何事件中断等待状态。 这可确保事件系统被唤醒时仍将正常工作。

下面的示例演示的实现[ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法。

```cpp
HRESULT _stdcall CWIADevice::drvNotifyPnpEvent(
  const GUID *pEventGUID,
  BSTR       bstrDeviceID,
  ULONG      ulReserved)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if ((!pEventGUID)||(!bstrDeviceID)) {
      return E_INVALIDARG;
  }

  HRESULT hr = S_OK;

  if(*pEventGUID == WIA_EVENT_POWER_SUSPEND) {

    //
    // disable any driver activity to make sure we properly
    // shut down (the driver is not being unloaded, just disabled)
    //

  } else if(*pEventGUID == WIA_EVENT_POWER_RESUME) {

    //
    // reestablish any event notifications to make sure we properly
    // set up any event waiting status using the WIA service supplied
    // event handle
    //

    if(m_EventOverlapped.hEvent) {

      //
      // call ourselves with the cached EVENT handle given to
      // the WIA driver by the WIA service.
      //

        SetNotificationHandle(m_EventOverlapped.hEvent);
    }
  }
  return hr;
}
```

 

 




