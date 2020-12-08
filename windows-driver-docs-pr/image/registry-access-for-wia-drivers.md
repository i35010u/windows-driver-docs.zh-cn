---
title: WIA 驱动程序的注册表访问权限
description: WIA 驱动程序的注册表访问权限
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f2b993fdcb7c9a39fc0b52ad30c78c57c8a9f96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817335"
---
# <a name="registry-access-for-wia-drivers"></a>WIA 驱动程序的注册表访问权限





驱动程序开发人员应该知道他们需要访问的注册表项的权限。 许多注册表都可供驱动程序读取。 但是，WIA 驱动程序只应写入在 [**IStiUSD：： Initialize**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize) 方法中传递给它们的注册表项。

虽然在 Windows XP 中可以写入到其他注册表项，但由于 WIA 服务在高特权 **LocalSystem** 帐户下运行，因此在 Microsoft Windows Server 2003 和更高版本中，这种情况下，不可能在低特权 **LocalService** 帐户下运行。

驱动程序通常需要对其注册表项（ **IStiUSD：： Initialize** 之外）的写入访问权限。 由于大多数驱动程序将数据存储在 **DeviceData** 子项中，因此可以轻松地打开 **DeviceData** 子项，并将句柄存储到打开的密钥，以备稍后使用。 仅当驱动程序不再需要此注册表项时，才应将其关闭。

下面的代码示例演示如何使用 **DeviceData** 注册表子项。

```cpp
STDMETHODIMP CWIADevice::Initialize(
  PSTIDEVICECONTROL   pIStiDevControl,
  DWORD               dwStiVersion,
  HKEY                hParametersKey)
{
  .
  .
  .
  //
  // Open the DeviceData key since this is where the
  // driver-specific settings will be stored.
  //
  DWORD dwError = RegOpenKeyEx(
                 hParametersKey,     // handle to open key
                 TEXT("DeviceData"), // subkey to open
                 0,                  // options (must be NULL)
                 KEY_READ|KEY_WRITE, // requesting read/write access
                 &m_hMyWritableRegistryKey);
  if (dwError == ERROR_SUCCESS)
  {
      //
      //  m_hMyWritableRegistryKey now contains a handle to the
      //  DeviceData subkey which can be used to store information
      //  in the registry.
      //  Notice that it isn't closed here, but instead,
      //  kept open because it is needed later.
     //
  }
  else 
  {
      // Handle error
      .
      .
      .
  }
  .
  .
  .
}

STDMETHODIMP CWIADevice::SomeDriverMethod()
{
  .
  .
  .
  //
  //  We need to store some setting in the registry here.
  //
  DWORD dwError = RegSetValueEx(
                     m_hMyWritableRegistryKey,
                     TEXT("MyDriverValueName"),
                     0,
                     REG_DWORD,
                     (BYTE*)&dwValue,
                     sizeof(dwValue));
  if (dwError == ERROR_SUCCESS)
  {
      //
      //  We successfully stored dwValue in the registry
      //
  }
  else 
  {
      // Handle error
      .
      .
      .
  }
  .
  .
  .
}

CWIADevice:: CWIADevice () :
  m_hMyWritableRegistryKey(NULL),
  .
  .
  .
{
  //  Rest of constructor goes here.  Ensure that the
  //   handle to the registry key is initialized to NULL.
}

CWIADevice::~CWIADevice(void)
{
  .
  .
  .
  //
  // If the writable registry key isn't closed  yet, do it now,
  // because the driver is about to be unloaded.
  //
  if (m_hMyWritableRegistryKey) 
  {
      RegCloseKey(m_hMyWritableRegistryKey);
      m_hMyWritableRegistryKey = NULL;
  }

  .
  .
  .
}
```

**DeviceData** 注册表子项在 windows Me、windows XP 和更高版本上可用于对驱动程序进行读/写访问。 设备密钥本身 (例如，对 **DeviceData**) 的父注册表项可能会打开，也可能不打开，这取决于操作系统版本。

**注意**   当不再需要驱动程序时，该驱动程序 *必须* 关闭它打开的任何注册表项，并且必须在卸载之前关闭所有注册表项。

 

 

