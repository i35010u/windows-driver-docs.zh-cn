---
title: 加载和卸载 WIA 微型驱动程序
description: 加载和卸载 WIA 微型驱动程序
ms.assetid: a5f930c3-f92c-498a-a334-b5eb60fbd61b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26978081c3a9afbb3d9e4a1fce13ca7a68033a5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546294"
---
# <a name="loading-and-unloading-a-wia-minidriver"></a>加载和卸载 WIA 微型驱动程序





WIA 的设备驱动程序安装后，WIA 服务会尝试将其加载第一次。 WIA 微型驱动程序的[ **IStiUSD::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff543824)方法调用，并且应执行以下任务：

1.  检查传输模式，以确定用于初始化此设备驱动程序的调用方的意图。 这是通过调用[ **IStiDeviceControl::GetMyDeviceOpenMode** ](https://msdn.microsoft.com/library/windows/hardware/ff542942)方法。

2.  获取已安装的设备的端口名称，以便此驱动程序可以调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858) （Microsoft Windows SDK 中所述） 上访问设备的正确端口。 这是通过调用[ **IStiDeviceControl::GetMyDevicePortName** ](https://msdn.microsoft.com/library/windows/hardware/ff542944)方法。

3.  读取设备安装过程中写入的特定于设备的注册表设置。 这可以通过使用*hParametersKey*参数传递给**IStiUSD::Initialize**。

WIA 服务调用**IStiUSD::Initialize**方法第一个驱动程序时加载。 **IStiUSD::Initialize**方法也称为客户端使用旧 STI DDIs 和调用时[ **IStillImage::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543778)方法。

**IStiUSD::Initialize**方法应初始化 WIA 驱动程序和适用于使用的设备。 WIA 驱动程序可以存储**IStiDeviceControl**如果它们在更高版本时需要的接口指针。 [ **IStiDeviceControl::AddRef** ](https://msdn.microsoft.com/library/windows/hardware/ff542933)存储此接口之前，必须在调用方法。 如果不需要存储接口，则忽略它。 不要*不*发行**IStiDeviceControl**接口，如果您不调用**IStiDeviceControl::AddRef**第一个。 这可能会导致不可预知的结果。 [IStiDeviceControl COM 接口](istidevicecontrol-com-interface.md)需获取有关设备的端口的信息。 对的调用中使用的端口名称[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数可以通过调用来获取**IStiDeviceControl::GetMyDevicePortName**方法。 共享端口，例如串行端口设备上的设备打开中的端口**IStiUSD::Initialize**不建议。 应仅在调用中打开该端口**IStiUSD::LockDevice**。 应在内部控制的端口的结束，以便快速访问。 (打开并在关闭**IStiUSD::LockDevice**并**IStiUSD::UnLockDevice**非常低效。 **CreateFile**可能会导致延迟导致设备出现缓慢甚至失去反应给用户。)

如果 WIA 驱动程序不能支持多个[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)调用在同一设备端口，则**IStiDeviceControl::GetMyDeviceOpenMode**应调用方法。

WIA 驱动程序应检查返回的模式值 STI\_设备\_创建\_数据标记，并相应地打开端口。

如果设备端口必须打开，则会调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)应使用。 打开一个端口，该文件时\_标志\_应使用 OVERLAPPED 标志。 这允许 OVERLAPPED 结构 （Windows SDK 文档中所述） 来访问设备时使用。 使用重叠的 I/O 可帮助控制响应式访问到的硬件。 WIA 驱动程序检测到问题时，可以调用**CancelIo** （Windows SDK 文档中所述） 若要停止当前的所有硬件访问。

下面的示例演示的实现**IStiUSD::Initialize**方法。

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

WIA 服务调用[ **IStiUSD::GetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543817)之后在成功调用**IStiUSD::Initialize**方法。 **IStiUSD::GetCapabilities**然后提供[ **STI\_美元\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff548404) STI 版本信息，WIA 支持标志 （位标志，指示结构驱动程序功能），以及任何事件要求。

下面的示例演示的实现**IStiUSD::GetCapabilities**。

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

 

 




