---
title: 演示如何初始化设备属性的代码示例
description: 演示如何初始化设备属性的代码示例
ms.assetid: ec25fa77-13d8-4cb0-913c-b24010355702
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0b69445392be4fcd71f456ab155373dd720460a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840873"
---
# <a name="code-example-for-initializing-device-properties"></a>演示如何初始化设备属性的代码示例


在 IWiaMiniDrv：为根项[ **:D rvinititemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)调用期间，微型驱动程序必须初始化以下描述设备的 WIA 属性：

[**WIA\_DPS\_服务\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-service-id)

[**WIA\_DPS\_设备\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-device-id)

[**WIA\_DP\_全局\_标识**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-global-identity)

[**WIA\_DPA\_固件\_版本**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-firmware-version)

下面的代码示例演示了如何使用**OpenProperyStore**和**READDEVICEPROPERTY**方法\_DPS\_SERVICE\_ID 初始化 WIA，以读取 PKEY\_PNPX\_ServiceId。 可以使用相同的常规方法来初始化每个设备属性。

```cpp
HRESULT hr = S_OK;
IPropertyStore *pPropertyStore = NULL;
BSTR bstrPropertyValue = NULL;

//
// Open the current Property Store and keep it opened until all needed properties are read
//
if (SUCCEEDED(hr))
{
    hr = OpenPropertyStore(&pPropertyStore);
    if (FAILED(hr))
    {
        WIAS_ERROR((g_hInst, "Failed to open the Property Store for the current Function Instance, hr = 0x%08X", hr));
    }
}

//
// Initialize WIA_DPS_SERVICE_ID
//
if (SUCCEEDED(hr))
{
    hr = ReadDeviceProperty(pPropertyStore, &PKEY_PNPX_ServiceId, &bstrPropertyValue);
    if (FAILED(hr))
    {
        WIAS_ERROR((g_hInst, "Failed to read the PKEY_PNPX_ServiceId device property, hr = 0x%08X", hr));
    }

    if ((SUCCEEDED(hr)) && (bstrPropertyValue)) 
    {
        WIAS_TRACE((g_hInst, "Service id: %ws", (LPWSTR)bstrPropertyValue));
 
        hr = AddProperty(WIA_DPS_SERVICE_ID, WIA_DPS_SERVICE_ID_STR, RN, bstrPropertyValue);
        if (FAILED(hr)) 
        {
            WIAS_ERROR((g_hInst, "Failed to add WIA_DPS_SERVICE_ID property to the property manager, hr = 0x%08X", hr));
        }
    }

    if (bstrPropertyValue)
    {
        SysFreeString(bstrPropertyValue);
        bstrPropertyValue = NULL;
    }
}

//
// Repeat the same procedure for WIA_DPS_DEVICE_ID, WIA_DPS_GLOBAL_IDENTITY, and WIA_DPS_FIRMWARE_VERSION
//

//
// Close the Property Store
//
if (pPropertyStore)
{
    pPropertyStore->Release();
    pPropertyStore = NULL;
}
```

 

 




