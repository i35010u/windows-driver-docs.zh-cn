---
title: 演示如何初始化设备属性的代码示例
description: 演示如何初始化设备属性的代码示例
ms.assetid: ec25fa77-13d8-4cb0-913c-b24010355702
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce393b129017cec2438e4a5fcf143fa1a06ba114
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191511"
---
# <a name="code-example-for-initializing-device-properties"></a>演示如何初始化设备属性的代码示例


在 IWiaMiniDrv：为根项 [**:D rvinititemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties) 调用期间，微型驱动程序必须初始化以下描述设备的 WIA 属性：

[**WIA \_ DPS \_ 服务 \_ ID**](./wia-dps-service-id.md)

[**WIA \_ DPS \_ 设备 \_ ID**](./wia-dps-device-id.md)

[**WIA \_ DPS \_ 全局 \_ 标识**](./wia-dps-global-identity.md)

[**WIA \_ DPA \_ 固件 \_ 版本**](./wia-dpa-firmware-version.md)

下面的代码示例演示了如何 \_ \_ \_ 使用 **OpenProperyStore** 和 **ReadDeviceProperty** 方法来读取 PKEY \_ PNPX ServiceId，从而初始化 WIA DPS 服务 ID \_ 。 可以使用相同的常规方法来初始化每个设备属性。

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

 

