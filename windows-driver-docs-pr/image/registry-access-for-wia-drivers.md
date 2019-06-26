---
title: WIA 驱动程序的注册表访问权限
description: WIA 驱动程序的注册表访问权限
ms.assetid: 0e0b7493-858b-4add-9e1d-fd71bae21b6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba2d916e2ce22f233f616c0fb503bbf8331b6262
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376491"
---
# <a name="registry-access-for-wia-drivers"></a>WIA 驱动程序的注册表访问权限





驱动程序开发人员应了解访问所需的注册表项的权限。 在注册表的大部分是可用于驱动程序进行读取。 但是，WIA 驱动程序应仅向传递给它们中的注册表项写入[ **IStiUSD::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)方法。

尽管因为 WIA 服务在高特权下运行在 Windows XP 中，可以写入其他注册表项**LocalSystem**帐户，这可不能再在低特权下**LocalService**帐户，在 Microsoft Windows Server 2003 和更高版本。

驱动程序通常需要对其注册表项之外的写访问权限**IStiUSD::Initialize**。 因为大多数驱动程序存储中的数据**DeviceData**子项，它可轻松打开**DeviceData**子项，并将存储到更高版本使用的打开密钥句柄。 仅当它不再需要该密钥时，该驱动程序应关闭注册表项。

下面的代码示例演示如何使用**DeviceData**注册表子项。

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

**DeviceData**注册表子项是打开 Windows Me 和 Windows XP 上的驱动程序的读/写访问和更高版本。 设备密钥本身 (例如，父注册表项**DeviceData**) 可能也不是打开以进行写访问由驱动程序，具体取决于操作系统版本。

**请注意**  驱动程序*必须*关闭时它们不再需要必须关闭所有注册表项之前卸载它打开任何注册表项。

 

 

 




