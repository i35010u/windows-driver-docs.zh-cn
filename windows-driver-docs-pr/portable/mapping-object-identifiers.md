---
Description: Mapping Object Identifiers
title: 将对象标识符映射
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86d2edebc8fbd0ff7704cdb47c2d68d942d0f543
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540487"
---
# <a name="mapping-object-identifiers"></a>将对象标识符映射


映射函数**WpdBaseDriver::OnGetObjectIDsFromPersistentUniqueIDs**，处理到持久标识符的对象标识符的映射。 在 WPD 驱动程序模型中，对象标识符是为给定的设备会话才有效的标识符。 设备的所有会话是有效的永久标识符。

以下内容摘自示例驱动程序包含的代码**WpdBaseDriver::OnGetObjectIDsFromPersistentUniqueIDs。**

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

某些设备可能存储在对象中的永久标识符、 一些可能会生成基于哈希对象数据的永久标识符和其他人可能会将其对象标识符作为持久标识符 （因为它们将永远不会更改）。 WpdHelloWorldDriver 示例实现此后一种情况。

当客户端应用程序调用**IPortableDeviceContent::GetObjectIDsFromPersistentUniqueIDs**方法，该驱动程序，都依次调用**WpdBaseDriver::OnGetObjectIDsFromPersistentUniqueIDs**.

 

 




