---
description: 映射对象标识符
title: 映射对象标识符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50431920ba55816acdc42b2b8d7b5ede6fbd1e37
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969552"
---
# <a name="mapping-object-identifiers"></a>映射对象标识符


Mapping 函数 **WpdBaseDriver：： OnGetObjectIDsFromPersistentUniqueIDs**处理对象标识符到永久性标识符的映射。 在 WPD 驱动程序模型中，对象标识符是仅对给定设备会话有效的标识符。 永久性标识符在所有设备会话中有效。

示例驱动程序的以下摘录包含**WpdBaseDriver：： OnGetObjectIDsFromPersistentUniqueIDs**的代码。

```ManagedCPlusPlus
HRESULT WpdBaseDriver::OnGetObjectIDsFromPersistentUniqueIDs(
    IPortableDeviceValues* pParams,
    IPortableDeviceValues* pResults)
{

    HRESULT hr      = S_OK;
    DWORD   dwCount = 0;
    CComPtr<IPortableDevicePropVariantCollection> pPersistentIDs;
    CComPtr<IPortableDevicePropVariantCollection> pObjectIDs;

    if((pParams    == NULL) ||
       (pResults   == NULL))
    {
        hr = E_POINTER;
        CHECK_HR(hr, "Cannot have NULL parameter");
        return hr;
    }

    // Get the list of Persistent IDs
    if (hr == S_OK)
    {
        hr = pParams->GetIPortableDevicePropVariantCollectionValue(WPD_PROPERTY_COMMON_PERSISTENT_UNIQUE_IDS, &pPersistentIDs);
        CHECK_HR(hr, "Failed to get WPD_PROPERTY_COMMON_PERSISTENT_UNIQUE_IDS");
    }

    // Create the collection to hold the ObjectIDs
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pObjectIDs);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Iterate through the persistent ID list and add the equivalent object ID for each element.
    if (hr == S_OK)
    {
        hr = pPersistentIDs->GetCount(&dwCount);
        CHECK_HR(hr, "Failed to get count from persistent ID collection");

        if (hr == S_OK)
        {
            DWORD       dwIndex        = 0;
            PROPVARIANT pvPersistentID = {0};
            PROPVARIANT pvObjectID     = {0};

            PropVariantInit(&pvPersistentID);
            PropVariantInit(&pvObjectID);

            for(dwIndex = 0; dwIndex < dwCount; dwIndex++)
            {
                pvObjectID.vt = VT_LPWSTR;
                hr = pPersistentIDs->GetAt(dwIndex, &pvPersistentID);
                CHECK_HR(hr, "Failed to get persistent ID at index %d", dwIndex);

                // Because our persistent unique identifiers are identical to our object
                // identifiers, we just return it back to the caller.
                if (hr == S_OK)
                {
                    pvObjectID.pwszVal = AtlAllocTaskWideString(pvPersistentID.pwszVal);
                }

                if (hr == S_OK)
                {
                    hr = pObjectIDs->Add(&pvObjectID);
                    CHECK_HR(hr, "Failed to add next Object ID");
                }

                PropVariantClear(&pvPersistentID);
                PropVariantClear(&pvObjectID);

                if(FAILED(hr))
                {
                    break;
                }
            }
        }
    }

    if (hr == S_OK)
    {
        hr = pResults->SetIPortableDevicePropVariantCollectionValue(WPD_PROPERTY_COMMON_OBJECT_IDS, pObjectIDs);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_COMMON_OBJECT_IDS");
    }

    return hr;
}
```

某些设备可能会在对象中存储永久性标识符，某些设备可能会根据对象数据的哈希生成永久性标识符，而其他设备可能会将其对象标识符视为永久性标识符 (因为它们永远不会更改) 。 WpdHelloWorldDriver 示例实现此后一种情况。

当客户端应用程序调用 **IPortableDeviceContent：： GetObjectIDsFromPersistentUniqueIDs** 方法时，驱动程序依次调用 **WpdBaseDriver：： OnGetObjectIDsFromPersistentUniqueIDs**。

 

 




