---
title: 添加中断事件支持
description: 添加中断事件支持
ms.assetid: 74fbaa7c-f058-4b17-b278-3dea0faf4431
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc71847b137e63962a8cc047c2e4dd6ef093d478
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840909"
---
# <a name="adding-interrupt-event-support"></a>添加中断事件支持





若要正确设置 WIA 驱动程序以报告中断事件，请执行以下操作：

1.  设置设备 INF 文件中的**0x31 =** 。 （有关详细信息，请参阅[用于 WIA 设备的 INF 文件](inf-files-for-wia-devices.md)。）

2.  Report STI\_GENCAP\_通知和 STI\_USD\_GENCAP\_[**PUSHSUPPORT：： IStiUSD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)方法中的本机\_GetCapabilities。

3.  报告[**IWiaMiniDrv：:D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法中所有受支持的事件。

4.  缓存并使用[**IStiUSD：： SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)方法中传递的事件句柄。 此事件句柄表示设备发出信号，或 WIA 微型驱动程序直接使用**SetEvent** （如 Microsoft Windows SDK 文档中所述）发出信号。 在此方法中，您将启动 WIA 设备的等待状态。

5.  在[**IStiUSD：： GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)方法中报告正确的事件信息响应。

以下两个示例演示如何将设备配置为具有**IWiaMiniDrv：:D rvgetcapabilities**和**IStiUSD：： SetNotificationHandle**方法的实现的中断。

**请注意**   对涉及内核模式驱动程序的所有活动使用重叠 i/o 调用非常重要。 这允许对设备请求进行适当的超时和取消操作。

 

### <a href="" id="explanation-of-the-iwiaminidrv-drvgetcapabilities-implementation"></a>IWiaMiniDrv：:d rvGetCapabilities 实现的说明

WIA 服务调用**IWiaMiniDrv：:D rvgetcapabilities**方法，以获取 WIA 设备支持的事件和命令。 WIA 驱动程序应该首先查看传入的*lFlags*参数，以确定应应答的请求。

WIA 驱动程序应分配内存（由 WIA 驱动程序使用并由其释放）以包含[**WIA\_DEV\_CAP\_winspool.drv**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_dev_cap_drv)结构的数组。 在对**IWiaMiniDrv：:D rvgetcapabilities**的调用中，在*ppCapabilities*参数中传递一个指针，该指针指向保存 WIA 驱动程序分配的内存地址的内存位置。

**请注意**   WIA 服务不会释放此内存。 WIA 驱动程序必须管理分配的内存，这一点很重要。

 

下面的示例演示[**IWiaMiniDrv：:D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法的实现。

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

WIA 服务调用[**IStiUSD：： SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)方法，或由该驱动程序在内部调用，以启动或停止事件通知。 WIA 服务将传入有效的句柄，该句柄使用**CreateEvent**创建（在 Microsoft Windows SDK 文档中介绍），指示 WIA 驱动程序在硬件中发生事件时向此句柄发送信号。

**NULL**可传递给**IStiUSD：： SetNotificationHandle**方法。 **NULL**表示 WIA 微型驱动程序要停止所有设备活动，并退出所有事件等待操作。

下面的示例演示**IStiUSD：： SetNotificationHandle**方法的实现。

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

如果 WIA 微型驱动程序或 WIA 设备检测到事件并发出信号，WIA 服务将调用[**IStiUSD：： GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)方法。 在此方法中，WIA 微型驱动程序应报告发生的事件的详细信息。

WIA 服务调用**IStiUSD：： GetNotificationData**方法来获取有关刚发出信号的事件的信息。 可以通过两个事件操作中的一个来调用**IStiUSD：： GetNotificationData**方法。

1.  **IStiUSD：： GetStatus**报告存在挂起的事件，方法是在[**STI\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status)结构中设置 STI\_EVENTHANDLING\_挂起标志。

2.  由**IStiUSD：： SetNotificationHandle**传入的*hEvent*句柄已通过硬件或通过调用**SetEvent** （如 Microsoft Windows SDK 文档中所述）发出信号。

WIA 驱动程序负责填写[**STINOTIFY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_stinotify)结构

下面的示例演示**IStiUSD：： GetNotificationData**方法的实现。

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

可以通过将**NULL**作为事件句柄传递来随时停止中断事件。 微型驱动程序应将此解释为信号，以停止硬件设备上的任何等待状态。

**请注意**   [**IWiaMiniDrv：:d rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法可以接收影响事件等待状态的电源管理事件。

 

WIA 服务调用**IWiaMiniDrv：:D rvnotifypnpevent**方法，并在系统即将置于睡眠状态时发送 WIA\_事件\_POWER\_挂起事件。 如果发生此调用，则设备可能已超出其等待状态。 睡眠状态会自动触发内核模式驱动程序，以退出任何等待状态以允许系统进入此关闭状态。 当系统从睡眠状态恢复时，WIA 服务会将 WIA\_事件发送\_POWER\_RESUME 事件。 此时，WIA 微型驱动程序必须重新建立中断事件等待状态。 有关睡眠状态的详细信息，请参阅[系统电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-states)和[设备电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)。

建议 WIA 微型驱动程序缓存最初传递到[**IStiUSD：： SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)方法的事件句柄，以便在系统从睡眠或休眠中唤醒时可以重复使用该事件句柄。

恢复系统后，WIA 服务不*会*调用**IStiUSD：： SetNotificationHandle**方法。 建议微型驱动程序调用其**IStiUSD：： SetNotificationHandle**方法，传递缓存的事件句柄。

WIA 服务在发生系统事件时调用**IWiaMiniDrv：:D rvnotifypnpevent**方法。 WIA 驱动程序应检查*pEventGUID*参数，以确定正在处理的事件。

必须处理的一些常见事件如下：

<a href="" id="wia-event-power-suspend"></a>WIA\_事件\_POWER\_挂起  
系统将进入挂起/休眠模式。

<a href="" id="wia-event-power-resume"></a>WIA\_事件\_POWER\_简历  
系统正在从挂起/睡眠模式唤醒。

WIA 驱动程序应在从挂起返回后还原任何事件中断等待状态。 这可确保在系统唤醒时事件仍将正常工作。

下面的示例演示[**IWiaMiniDrv：:D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法的实现。

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

 

 




