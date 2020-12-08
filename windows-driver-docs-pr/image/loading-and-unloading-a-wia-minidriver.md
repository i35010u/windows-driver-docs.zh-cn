---
title: 加载和卸载 WIA 微型驱动程序
description: 加载和卸载 WIA 微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 625c3b143ef79da383d9558d34b4d2c7471e878e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824111"
---
# <a name="loading-and-unloading-a-wia-minidriver"></a>加载和卸载 WIA 微型驱动程序





安装 WIA 设备驱动程序后，WIA 服务将尝试首次加载该驱动程序。 WIA 微型驱动程序的 [**IStiUSD：： Initialize**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize) 方法被调用，并应执行以下任务：

1.  检查传输模式，确定调用方的初始化此设备驱动程序的意图。 这是通过调用 [**IStiDeviceControl：： GetMyDeviceOpenMode**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceopenmode) 方法来完成的。

2.  获取已安装设备的端口名称，使此驱动程序可以调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) (记录在 Microsoft Windows SDK) 上的相应端口上，以访问设备。 这是通过调用 [**IStiDeviceControl：： GetMyDevicePortName**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname) 方法来完成的。

3.  读取设备安装过程中写入的特定于设备的注册表设置。 这可以通过使用传递到 **IStiUSD：： Initialize** 的 *hParametersKey* 参数来完成。

首次加载驱动程序时，WIA 服务将调用 **IStiUSD：： Initialize** 方法。 当客户端使用旧版 STI DDIs 并调用 [**IStillImage：： CreateDevice**](/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))方法时，也会调用 **IStiUSD：： Initialize** 方法。

**IStiUSD：： Initialize** 方法应初始化 WIA 驱动程序和设备以供使用。 WIA 驱动程序可以在以后需要时存储 **IStiDeviceControl** 接口指针。 在存储此接口之前，必须先调用 [**IStiDeviceControl：： AddRef**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-addref) 方法。 如果不需要存储接口，则将其忽略。 如果 *尚未先* 调用 **IStiDeviceControl：： AddRef** ，请不要释放 **IStiDeviceControl** 接口。 这可能会导致不可预知的结果。 需要 [ISTIDEVICECONTROL COM 接口](istidevicecontrol-com-interface.md) ，才能获取有关设备端口的信息。 可以通过调用 **IStiDeviceControl：： GetMyDevicePortName** 方法来获取对 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)函数的调用中使用的端口名称。 对于共享端口上的设备，如串行端口设备，不建议在 **IStiUSD：： Initialize** 中打开端口。 仅应在对 **IStiUSD：： LockDevice** 的调用中打开端口。 应在内部控制端口的关闭，以提供快速访问。  (在 **IStiUSD：： LockDevice** 和 **IStiUSD：： UnLockDevice** 中打开和关闭的操作非常低效。 **CreateFile** 可能会导致设备出现慢且无法响应用户的延迟。 ) 

如果 WIA 驱动程序不能支持同一设备端口上的多个 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 调用，则应调用 **IStiDeviceControl：： GetMyDeviceOpenMode** 方法。

WIA 驱动程序应检查返回的 STI \_ 设备 \_ CREATE DATA 标志的模式值 \_ 并相应地打开端口。

如果必须打开设备端口，则应使用对 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 的调用。 打开端口时， \_ 应使用文件标志 \_ 重叠标志。 这允许在访问设备时使用 Windows SDK 文档) 中描述的重叠结构 (。 使用重叠 i/o 有助于控制对硬件的响应性访问。 当检测到问题时，WIA 驱动程序可以调用 Windows SDK 文档) 中所述的 **CancelIo** (来停止所有当前的硬件访问。

下面的示例演示 **IStiUSD：： Initialize** 方法的实现。

```cpp
STDMETHODIMP CWIADevice::Initialize(
  PSTIDEVICECONTROL   pIStiDeviceControl,
  DWORD               dwStiVersion,
  HKEY                hParametersKey)
{
  if (!pIStiDeviceControl) {
      return STIERR_INVALID_PARAM;
  }

  HRESULT hr = S_OK;

  //
  // Get the mode of the device to check why we were created.  status, data, or both...
  //

  DWORD dwMode = 0;
  hr = pIStiDeviceControl->GetMyDeviceOpenMode(&dwMode);
  if(FAILED(hr)){
      return hr;
  }

  if(dwMode & STI_DEVICE_CREATE_DATA)
  {
      //
      // device is being opened for data
      //
  }

  if(dwMode & STI_DEVICE_CREATE_STATUS)
  {
      //
      // device is being opened for status
      //
  }

  if(dwMode & STI_DEVICE_CREATE_BOTH)
  {
      //
      // device is being opened for both data and status
      //
  }

  //
  // Get the name of the device port to be used in a call to CreateFile().
  //

  WCHAR szDevicePortNameW[MAX_PATH];
  memset(szDevicePortNameW,0,sizeof(szDevicePortNameW));

  hr = pIStiDeviceControl->GetMyDevicePortName(szDevicePortNameW,
                                            sizeof(szDevicePortNameW)/sizeof(WCHAR));
  if(FAILED(hr)) {
      return hr;
  }

  //
  // Open kernel-mode device driver. Use the FILE_FLAG_OVERLAPPED flag 
  // for proper cancellation
  // of kernel-mode operations and asynchronous file IO. 
  //  The CancelIo() call will function properly if this flag is used.
  //  It is recommended to use this flag.
  //

  m_hDeviceDataHandle = CreateFileW(szDevicePortNameW,
                                   GENERIC_READ | GENERIC_WRITE, // Access mask
                                   0,                            // Share mode
                NULL,                         // SA
                                   OPEN_EXISTING,                // Create disposition
                                   FILE_ATTRIBUTE_SYSTEM|FILE_FLAG_OVERLAPPED,
                                   NULL );

  m_dwLastOperationError = ::GetLastError();

  hr = (m_hDeviceDataHandle != INVALID_HANDLE_VALUE) ?
              S_OK : MAKE_HRESULT(SEVERITY_ERROR,FACILITY_WIN32,m_dwLastOperationError);

  if (FAILED(hr)) {
      return hr;
  }

  //
  // Open DeviceData section to read driver specific information
  //

  HKEY hKey = hParametersKey;
  HKEY hOpenKey = NULL;
  if (RegOpenKeyEx(hKey,                     // handle to open key
                   TEXT("DeviceData"),       // address of name of subkey to open
                   0,                        // options (must be NULL)
                   KEY_QUERY_VALUE|KEY_READ, // just want to QUERY a value
                   &hOpenKey                 // address of handle to open key
     ) == ERROR_SUCCESS) {

      //
      // This is where you read registry entries for your device.
      // The DeviceData section is the proper place to put this 
      // information. Information about your device should
      // have been written using the WIA device's .INF installation
      // file.
      // You can access this information from this location in the
      // Registry. The WIA service owns the hParameters HKEY. 
      // DO NOT CLOSE THIS KEY. Always close any HKEYS opened by
      //  this WIA driver after you are finished.
      //

      //
      // close registry key when finished, reading DeviceData information.
      //

      RegCloseKey(hOpenKey);
  } else {
      return E_FAIL;
  }
  return hr;
}
```

WIA 服务在成功调用 **IStiUSD：： Initialize** 方法后调用 [**IStiUSD：： GetCapabilities**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities) 。 **IStiUSD：： GetCapabilities** 提供 [**STI \_ USD \_ CAP**](/windows-hardware/drivers/ddi/stiusd/ns-stiusd-_sti_usd_caps) 结构，其中包含 STI 版本信息，WIA 支持标志 (位标志，指示驱动程序功能) 和所有事件要求。

下面的示例演示 **IStiUSD：： GetCapabilities** 的实现。

```cpp
/********************************************************************\
* CWIADevice::GetCapabilities
* Remarks:
* This WIA driver sets the following capability flags:
* 1. STI_GENCAP_WIA - This driver supports WIA
* 2. STI_USD_GENCAP_NATIVE_PUSHSUPPORT - This driver supports push
*    buttons
* 3. STI_GENCAP_NOTIFICATIONS - This driver requires the use of 
*    interrupt events.
*
\********************************************************************/

STDMETHODIMP CWIADevice::GetCapabilities(PSTI_USD_CAPS pUsdCaps)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pUsdCaps) {
      return E_INVALIDARG;
  }

  memset(pUsdCaps, 0, sizeof(STI_USD_CAPS));
  pUsdCaps->dwVersion     = STI_VERSION;    // STI version
  pUsdCaps->dwGenericCaps = STI_GENCAP_WIA| // WIA support
                            STI_USD_GENCAP_NATIVE_PUSHSUPPORT| // button support
                            STI_GENCAP_NOTIFICATIONS; // interrupt event support
  return S_OK;
}
```

 

