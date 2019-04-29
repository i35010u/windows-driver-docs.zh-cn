---
title: 创建一个传感器的永久唯一标识符
description: 创建一个传感器的永久唯一标识符
ms.assetid: 09ff583e-6bb5-4812-ae3b-970dac671e39
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: daf3b932db347aaf732742a032c88deeb39dab9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382122"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor"></a>创建一个传感器的永久唯一标识符


您的驱动程序必须创建每个传感器的永久唯一标识符 (PUID)。 PUID 是存储在会话之间并唯一地标识在设备上的对象的 GUID 值。 您的驱动程序必须返回 PUID 值查询的名为传感器的属性时\_属性\_的永久\_UNIQUE\_id。 如果设备包含多个传感器，则必须自己 PUID 分配每个传感器。 应用程序可以通过调用来检索此 ID [ISensor::GetID](https://go.microsoft.com/fwlink/p/?linkid=157812)传感器 API 中的方法。

您应创建新 PUID 为每个传感器，当传感器首次连接到计算机，，然后存储以供将来使用此值。

您的驱动程序应创建或传感器类扩展在初始化之前，例如，调用时检索 PUID [ **IPnpCallbackHardware::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556766)。 此方法提供一个指向[IWDFDevice](https://msdn.microsoft.com/library/windows/hardware/ff556917)表示传感器的接口。 此指针可用于访问每个设备的特定属性存储。

下面的代码示例根据需要创建一个函数，创建、 存储和检索 PUID。

```cpp
// Sets the persistent unique ID property in the WDF property store
// and returns the GUID for use in PortableDeviceValues property bags.
HRESULT CMyDevice::GetUniqueID(__in IWDFDevice* pWdfDevice,
                                            __in LPCWSTR wszSensorID, __out GUID* puid)
{
    HRESULT hr = S_OK;

    // Smart pointer to the WDF property store.
    // This pointer can store or retrieve the ID.
    CComPtr<IWDFNamedPropertyStore> spPropStore;
    if (SUCCEEDED(hr))
    {
        // Create the property store for this device or
        // retrieve the existing one.
        hr = pWdfDevice->RetrieveDevicePropertyStore(NULL, WdfPropertyStoreCreateIfMissing, &spPropStore, NULL);
    }

    if(SUCCEEDED(hr))
    {
        GUID idGuid;

        PROPVARIANT vID;

        // Try to get the PUID value previously stored as a string.
        hr = spPropStore->GetNamedValue(wszSensorID, &vID);
        if (SUCCEEDED(hr))
        {
            // Convert the PUID string to a GUID.
            hr = ::CLSIDFromString(vID.bstrVal, &idGuid);
        }
        else
        {
            // There was no value in the store, so create a new value.
            hr = ::CoCreateGuid(&idGuid);

            if (SUCCEEDED(hr))
            {
                // Convert the GUID to a string.
                LPOLESTR lpszGUID = NULL;
                hr = ::StringFromCLSID(idGuid, &lpszGUID);
                if (SUCCEEDED(hr))
                {
                    // Put the new value into the property store.
                    PropVariantInit(&vID);
                    vID.vt = VT_LPWSTR;
                    vID.pwszVal = lpszGUID;
                    hr = spPropStore->SetNamedValue(wszSensorID, &vID);
                    PropVariantClear(&vID);
                }
            }
        }

        // Return the PUID GUID.
        *puid = idGuid;
    }

    return hr;
}
```

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](https://msdn.microsoft.com/library/windows/hardware/hh768273)



