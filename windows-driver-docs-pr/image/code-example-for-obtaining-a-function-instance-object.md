---
title: 用于获取函数实例对象的代码示例
description: 用于获取函数实例对象的代码示例
ms.assetid: d4e3c5e0-d904-4049-9bc2-6c21d2a6f905
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d128dc66ea205734f4e807ecedc9ce2e98c558d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562158"
---
# <a name="code-example-for-obtaining-a-function-instance-object"></a>用于获取函数实例对象的代码示例


下面的代码示例包含示例类 (CWSDDevice)，包含与获取当前函数实例对象相关的两个类成员的声明：

-   CWSDDevice::m\_pFunctionDiscovery

-   CWSDDevice::m\_pFunctionInstance

代码示例还演示方法来初始化这些成员和方法来从当前函数实例属性存储中读取设备属性。 **CWSDDevice::InitializeConnection**方法说明中所述的过程[获取函数实例对象](obtaining-a-function-instance-object.md)若要获取表示当前函数实例对象当前的 web 服务扫描程序设备实例。

```cpp
/**************************************************************************\
* Sample CWSDDevice class that encapsulates the device communication interface 
\**************************************************************************/

class CWSDDevice
{
public:

    CWSDDevice();

    ~CWSDDevice();

    HRESULT 
    InitializeConnection(
        __in LPCWSTR wszDevicePath);

    HRESULT 
    UnInitializeConnection();

    HRESULT
    OpenPropertyStore(
        __out IPropertyStore **ppPropertyStore);

    HRESULT
    ReadDeviceProperty(
        __in_opt IPropertyStore *pPropertyStore,
        __in const PROPERTYKEY  *pPropertyKey,
        __out BSTR              *pbstrPropertyValue);

private:

    //
    // Flag indicating successful initialization was performed:
    //
    BOOL m_bInitialized;
 
    //
    // Function Discovery object
    //
    IFunctionDiscovery *m_pFunctionDiscovery;

    //
    // Function Instance object (which represents the current device instance)
    //
    IFunctionInstance *m_pFunctionInstance;
};

/**************************************************************************\
* CWSDDevice::InitializeConnection
*
* Initializes the connection to the web services scanner through Function Discovery
*
* Arguments:
*
*    wszDevicePath - unique PNPX ID identifier for the WS scanner, 
*                    returned by IStiDeviceControl::GetMyDevicePortName 
*
* Return Value:
*
*    S_OK if successful, an error HRESULT otherwise
*
\**************************************************************************/

HRESULT InitializeConnection(
    __in LPCWSTR wszDevicePath)
{
    HRESULT                           hr                 = S_OK;
    IFunctionInstanceCollectionQuery *pfiCollectionQuery = NULL;
    IFunctionInstanceCollection      *pfiCollection      = NULL;
    PROPVARIANT                       PropVar            = {0};

    if (m_bInitialized)
    {
        //
        // Initialization was performed once. Treat this is as a
        // re-initialization request: un-initialize and initialize again:
        //
        hr = UnInitialize();
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "Failed to re-initialize device interface, hr = 0x%08X", hr));
        }
    }

    if (!wszDevicePath)
    {
        hr = E_INVALIDARG;
        WIAS_ERROR((g_hInst, "Failed to initialize device interface, invalid device path argument, hr = 0x%08X", hr));
    }

    if (SUCCEEDED(hr))
    {
        PropVariantInit(&PropVar);
        PropVar.vt = VT_LPWSTR;
        PropVar.pwszVal = (LPWSTR)wszDevicePath;
    }

    if (SUCCEEDED(hr))
    {
        //
        // Create the Function Discovery object
        //
        hr = CoCreateInstance(__uuidof(FunctionDiscovery),
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              __uuidof(IFunctionDiscovery),
                              (void**)&m_pFunctionDiscovery);

        if ((SUCCEEDED(hr)) && (!m_pFunctionDiscovery))
        {
            hr = E_POINTER;
            WIAS_ERROR((g_hInst, "CoCreateInstance(IFunctionDiscovery) returned a NULL m_pFunctionDiscovery, hr = 0x%08X", hr));
        }
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "CoCreateInstance for IFunctionDiscovery failed, hr = 0x%08X", hr));
        }

    }

    if (SUCCEEDED(hr))
    {
        //
        // Query the Function Discovery object for a collection of
        // Function Instances that are related to this device path
        //
        hr = m_pFunctionDiscovery->CreateInstanceCollectionQuery(FCTN_CATEGORY_PNP,
                                                                 NULL,
                                                                 FALSE,
                                                                 NULL, 
                                                                 &pfiCollectionQuery);
        if ((SUCCEEDED(hr)) && (!pfiCollectionQuery))
        {
            WIAS_ERROR((g_hInst, 
                "IFunctionDiscovery::CreateInstanceCollectionQuery(%ws) returned a NULL IFunctionInstanceCollectionQuery* with hr = 0x%08X", 
                FCTN_CATEGORY_PNP, hr));
            hr = E_POINTER;
        }
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "IFunctionDiscovery::CreateInstanceCollectionQuery(%ws) failed, hr = 0x%08X", FCTN_CATEGORY_PNP, hr));
        }
    }

    if (SUCCEEDED(hr))
    {
        //
        // Pass in the device path (which contains a PnP-X ID) as a query constraint to the new collection query
        //
        hr = pfiCollectionQuery->AddPropertyConstraint(PKEY_PNPX_ID, &PropVar, QC_EQUALS);

        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "IFunctionInstanceCollectionQuery::AddPropertyConstraint(PKEY_PNPX_ID, %ws) failed, hr = 0x%08X", 
                wszDevicePath, hr));
        }
    }

    if (SUCCEEDED(hr))
    {
        //
        // Execute the query to obtain the unique Function Instance object that identifies our device that is described by wszDevicePath
        //
        hr = pfiCollectionQuery->Execute(&pfiCollection);

        if ((SUCCEEDED(hr)) && (!pfiCollection))
        {
            hr = E_POINTER;
            WIAS_ERROR((g_hInst, 
                "IFunctionInstanceCollectionQuery::Execute returned a NULL IFunctionInstanceCollection* for %ws, hr = 0x%08X",
                wszDevicePath, hr));
        }

        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "IFunctionInstanceCollectionQuery::Execute for DevicePath %ws failed, hr = 0x%08X", 
                wszDevicePath, hr));
        }
    }

    if (SUCCEEDED(hr))
    {
        //
        // Retrieve the unique Function Instance object that identifies our device
        //
        // Note that after the IFunctionDiscovery::CreateInstanceCollectionQuery constraint 
        // the collection must contain a single element, accessible by pfiCollection->Item(0).
        //
        // Without the query constraint, we must search for the Function Instance that corresponds 
        // to our wszDevicePath in the entire collection, using pfiCollection->Count and pfiCollection->Item...
        //
        // See the IFunctionInstanceCollection interface that is defined in FunctionDiscoveryAPI.idl
        //
        //     interface IFunctionInstanceCollection : IUnknown
        //     {
        //         HRESULT GetCount(
        //             [out, retval] DWORD * pdwCount);
        //
        //         HRESULT Item(
        //             [in] DWORD dwIndex,
        //             [out, retval] IFunctionInstance ** ppFunctionInstance);
        //     };
        //
        //

        hr = pfiCollection->Item(0, &m_pFunctionInstance);

        if ((SUCCEEDED(hr)) && (!m_pFunctionInstance))
        {
            WIAS_ERROR((g_hInst, "IFunctionInstanceCollection.Item(0) returned a NULL IFunctionInstance* for %ws with hr = 0x%08X", 
                wszDevicePath, hr));
            hr = E_POINTER;
        }

        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "IFunctionInstanceCollection.Item(0) for %ws failed, hr = 0x%08X", wszDevicePath, hr));
        }
    }

    if (pfiCollection)
    {
        pfiCollection->Release();
        pfiCollection = NULL;
    }

    if (pfiCollectionQuery)
    {
        pfiCollectionQuery->Release();
        pfiCollectionQuery = NULL;
    }

    if (SUCCEEDED(hr))
    {
        WIAS_TRACE((g_hInst, "Device interface successfully initialized", hr));
    }

    if (SUCCEEDED(hr))
    {
        m_bInitialized = TRUE;
    }
    else
    {
        UnInitialize();
    }

    return hr;
}

/**************************************************************************\
* CWSDDevice::UnInitializeConnection
*
* Uninitializes the connection to the web services scanner device
* through Function Discovery.
*
* Arguments:
*
*    none
*
* Return Value:
*
*    S_OK if successful, an error HRESULT otherwise
*
\**************************************************************************/

HRESULT CWSDDevice::UnInitializeConnection()
{
    HRESULT hr = S_OK;

    WIAS_TRACE((g_hInst, "Shutting down the current device connection, if any.."));

    //
    // Release Function Discovery COM interfaces:
    //

    if (m_pFunctionInstance)
    {
        m_pFunctionInstance->Release();
        m_pFunctionInstance = NULL;
    }

    if (m_pFunctionDiscovery)
    {
        m_pFunctionDiscovery->Release();
        m_pFunctionDiscovery = NULL;
    }


    m_bInitialized = FALSE;

    return hr;
}

/**************************************************************************\
* CWSDDevice::CWSDDevice
*
* Constructor for the CWSDDevice class that encapsulates the communication
* interface to the web services-compliant scanner image acquisition device 
*
* Arguments:
*
*   None
*
* Return Value:
*
*   None
*
\**************************************************************************/

CWSDDevice::CWSDDevice()
{
    m_pFunctionDiscovery = NULL;
    m_pFunctionInstance = NULL;

    m_bInitialized = FALSE;

    return;
}

/**************************************************************************\
* CWSDDevice::~CWSDDevice
*
* Destructor for the CWSDDevice class that encapsulates the communication
* interface to the web services-compliant scanner image acquisition device
*
* Arguments:
*
*   None
*
* Return Value:
*
*   None
*
\**************************************************************************/

CWSDDevice::~CWSDDevice()
{
    UnInitializeConnection();
    return;
};
```

 

 




