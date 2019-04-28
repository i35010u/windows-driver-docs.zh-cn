---
title: 引发传感器事件
description: 引发传感器事件
ms.assetid: a6e428f8-1613-4e8d-813d-5a54824dab82
keywords:
- 传感器事件
- 事件处理程序 (event handler)
- 数据更新事件
- 传感器数据更新事件
- 状态更改事件
- 传感器状态更改事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e49f2feb782430b31fcdc110d4a231ffa4f5408
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330061"
---
# <a name="raising-sensor-events"></a>引发传感器事件


有关传感器事件的工作原理的详细信息，请参阅[有关传感器驱动程序事件](about-sensor-driver-events.md)。

下面的代码示例演示引发数据更新和状态更改事件的类。 此类命名**CSensorManager**。

### <a name="member-variables"></a>成员变量

此类定义以下成员变量。

```c
// Smart pointer to the sensor class extension object.
CComPtr<ISensorClassExtension> m_spSensorCXT;

// Pointer to the callback class that the class extension calls.
CSensorDdi* m_pDdi;

// The event thread handle
HANDLE m_hEventThread;

// Handle to an event used to signal the thread to close.
HANDLE m_hCloseThread;

// The current report interval.
DWORD m_dwInterval;
```

### <a name="global-variables"></a>全局变量

该驱动程序会定义此类使用以下全局变量。

```c
// Sensor ID
static const LPWSTR g_wszSensorID = L"My Sensor ID";

// Default event interval
static const DWORD g_dwDefaultInterval = 1000; // one second
```

### <a name="lifetime-management"></a>生存期管理

回调类，名为 CSensorDdi，实现[ISensorDriver](https://msdn.microsoft.com/library/windows/hardware/ff545566)，第一个客户端订阅的事件时创建 CSampleEvents 事件类的实例。 客户端无法再订阅事件时，回调类将销毁 CSampleEvents 实例。

CSampleEvents 回拨到 CSensorDdi 要检索的最新的数据使用的相同方法，此类扩展使用，如[ **ISensorDriver::OnGetDataFields**](https://msdn.microsoft.com/library/windows/hardware/ff545607)。

下面的代码示例包含 CSampleEvents 事件类的方法实现。

```c
CSampleEvents::CSampleEvents()
{
    // Initialize member variables.
    m_hEventThread = NULL;
    m_hCloseThread = NULL;
    m_dwInterval = g_dwDefaultInterval;
};

CSampleEvents::~CSampleEvents()
{
};

// Initialize
// Sets the pointers to the class extension and the callback class.
HRESULT CSampleEvents::Initialize(ISensorClassExtension *pSensorCXT, CSensorDdi* pDdi)
{
    HRESULT hr = S_OK;

    if(NULL == pSensorCXT || NULL == pDdi)
    {
        return E_POINTER;
    }

    // Cache the pointers to the class extension and DDI callback class.
    m_spSensorCXT = pSensorCXT;
    m_pDdi = pDdi;

    // Create the event used to close the thread.
    m_hCloseThread = ::CreateEvent(NULL, FALSE, FALSE, TEXT("CloseThreadEvent"));

    if(NULL == m_hCloseThread)
    {
        hr = E_UNEXPECTED;
    }

    if(SUCCEEDED(hr))
    {
        m_hEventThread = ::CreateThread(NULL,   // Cannot be inherited by child process
                     0,                                       // Default stack size
                     &CSampleEvents::_EventThreadProc,     // Thread proc
                     (LPVOID)this,                            // Thread proc argument
                     0,                                       // Starting state = running
                     NULL);                                   // No thread identifier

        if(NULL == m_hEventThread)
        {
            hr = E_UNEXPECTED;
        }
    }

    return hr;
};

// Uninitializes the event class.
HRESULT CSampleEvents::Uninitialize()
{
    HRESULT hr = S_OK;

    // Stop the event thread.
    ::SetEvent(m_hCloseThread);

    // Wait for the thread to end.
    ::WaitForSingleObject(m_hEventThread, INFINITE);

    if (NULL != m_hEventThread)
    {
        CloseHandle(m_hEventThread);
        m_hEventThread = NULL;
    }

    if(NULL != m_hCloseThread)
    {
        CloseHandle(m_hCloseThread);
        m_hCloseThread = NULL;
    }

    // After Uninitialize, clients must call Initialize to set new pointers.
    m_pDdi = NULL;
    m_spSensorCXT.Release();

    return hr;
};

// Post a state change event
HRESULT CSampleEvents::PostStateEvent()
{
    HRESULT hr = (NULL == m_spSensorCXT) ? E_UNEXPECTED : S_OK ;

    if (SUCCEEDED(hr))
    {
        SensorState st;
        hr = m_pDdi->GetSensorState(&st);

        if (SUCCEEDED(hr))
        {
            // Post the state change event.
            hr = m_spSensorCXT->PostStateChange(g_wszSensorID, st);
        }
    }

    return hr;
}

// Post a data updated event
HRESULT CSampleEvents::PostDataEvent(IPortableDeviceValues* pValues)
{
    HRESULT hr = (NULL == m_spSensorCXT) ? E_UNEXPECTED : S_OK ;

    if (SUCCEEDED(hr))
    {
        CComPtr<IPortableDeviceValuesCollection> spValuesCollection;
        hr = spValuesCollection.CoCreateInstance(CLSID_PortableDeviceValuesCollection);

        if (SUCCEEDED(hr))
        {
            hr = spValuesCollection->Add(pValues);

            if (SUCCEEDED(hr))
            {
                hr = m_spSensorCXT->PostEvent(g_wszSensorID, spValuesCollection);
            }
        }
    }

    return hr;
}
```

### <a name="thread-procedure"></a>线程过程

下面的代码示例显示使用 CSampleEvents 类来引发数据更新事件的线程过程。

```c
DWORD WINAPI CSampleEvents::_EventThreadProc(__in LPVOID pvData)
{
// Cast the argument to the correct type.
 CSampleEvents* pThis = static_cast<CSampleEvents*>(pvData);

// New threads must always CoInitialize...
    HRESULT hr = CoInitializeEx(NULL, COINIT_MULTITHREADED);

    if (SUCCEEDED(hr))
    {
        // Wait loop timed to use current report interval.
        while (WAIT_TIMEOUT == WaitForSingleObject(pThis->m_hCloseThread, pThis->m_dwInterval))
        {
            if(NULL == pThis->m_pDdi ||
               NULL == pThis->m_spSensorCXT.p)
            {
                Trace(TRACE_LEVEL_ERROR, "%!FUNC!: NULL pointer in helper function.");
                hr = E_POINTER;
            }

            CComPtr<IPortableDeviceValues> spEventParams;
            CComPtr<IPortableDeviceKeyCollection> spKeys;

            if(SUCCEEDED(hr))
            {
                // Use the Ddi class to create the key collection.
                hr = pThis->m_pDdi->OnGetSupportedDataFields(g_wszSensorID, &spKeys);
            }

            if(SUCCEEDED(hr))
            {
                CComPtr<IWDFFile> spTemp;

                // Get the data fields.
                // Note that we're using a DDI call as a helper function, here.
                // Setting the first parameter to NULL will be problematic if you
                // choose to track or use IWDFFile pointers in OnGetDataFields.
                // This sample does not do so, therefore this is a safe thing to do
                // in this code.
                hr = pThis->m_pDdi->OnGetDataFields(spTemp, g_wszSensorID, spKeys,
                                                              &spEventParams);
            }

            if(SUCCEEDED(hr))
            {
                // Add the data event property key.
                hr = spEventParams->SetGuidValue(SENSOR_EVENT_PARAMETER_EVENT_ID,
                                                                SENSOR_EVENT_DATA_UPDATED);

                if(SUCCEEDED(hr))
                {
                    // Post the event.
                    hr = pThis->PostDataEvent(spEventParams);
                }
            }
        }
    }

 CoUninitialize();

    return SUCCEEDED(hr) ? 0 : 1;
};
```

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



