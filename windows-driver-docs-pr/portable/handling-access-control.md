---
Description: Handling Access Control
title: 处理访问控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31fdd53b47f4d7e762368ca571209967beb9e23a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544715"
---
# <a name="handling-access-control"></a>处理访问控制


WPD 驱动程序必须验证 WPD 命令有效负载已发送具有正确的 I/O 控制代码 (IOCTL) 以确保 I/O 管理器执行适当的 ACL 检查。 每个驱动程序必须执行此验证，因为 WPD 提供宏来自动执行该过程。

文件中定义这些宏*PortableDevice.h*。 它们是下表中所述。

| 宏                                            | 描述                                                                                                                                  |
|--------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 开始\_WPD\_命令\_访问\_映射                 | 定义命令访问表的开头。                                                                                           |
| 声明\_验证\_WPD\_命令\_访问            | 声明用于验证给定的 WPD 命令使用适当的访问权限标记在 IOCTL 发送该函数的实例。 |
| 声明\_WPD\_标准\_命令\_访问\_条目 | 声明的所有标准 WPD 命令中包含的条目*PortableDevice.h*。                                                 |
| 结束\_WPD\_命令\_访问\_映射                   | 定义命令访问表的末尾。                                                                                                 |
| 是\_WPD\_IOCTL                                   | 确定给定的 IOCTL 是特定于 WPD。                                                                                         |
| 验证是否\_WPD\_命令\_访问                     | 比较给定的 IOCTL 和针对一个驱动程序模块中定义的命令访问表及其参数。                     |
| WPD\_命令\_访问\_条目                      | 将自定义条目添加到命令访问表。                                                                                             |

 

在示例驱动程序，在中执行的访问控制验证**CQueue::OnDeviceIoControl**并**CQueue::ProcessWpdMessage**方法。 这些方法都位于*Queue.cpp*文件。 此外，此文件包含的命令访问表，列出了 WPD，以及任何自定义 Ioctl 和及其访问级别。

```ManagedCPlusPlus
// Add table used to lookup the Access required for Wpd Commands
BEGIN_WPD_COMMAND_ACCESS_MAP(g_WpdCommandAccessMap)
    DECLARE_WPD_STANDARD_COMMAND_ACCESS_ENTRIES
    // Add any custom commands here e.g.
    // WPD_COMMAND_ACCESS_ENTRY(MyCustomCommand, WPD_COMMAND_ACCESS_READWRITE)
END_WPD_COMMAND_ACCESS_MAP

// This allows driver developers to use VERIFY_WPD_COMMAND_ACCESS to check command access function for us.
DECLARE_VERIFY_WPD_COMMAND_ACCESS;
```

**OnDeviceIoControl**方法使用 IS\_WPD\_IOCTL 宏来标识 WPD Ioctl，并处理通过调用**ProcessWpdMessage**方法。

```ManagedCPlusPlus
STDMETHODIMP_ (void)
CQueue::OnDeviceIoControl(
        /* [in] */ IWDFIoQueue*     pQueue,
        /* [in] */ IWDFIoRequest*   pRequest,
        /* [in] */ ULONG            ControlCode,
        /* [in] */ SIZE_T           InputBufferSizeInBytes,
        /* [in] */ SIZE_T           OutputBufferSizeInBytes
        )
{
    HRESULT hr              = S_OK;
    DWORD   dwBytesWritten  = 0;

    if(IS_WPD_IOCTL(ControlCode))
    {
        BYTE*       pInputBuffer         = NULL;
        SIZE_T      cbInputBuffer        = 0;
        BYTE*       pOutputBuffer        = NULL;
        SIZE_T      cbOutputBuffer       = 0;
        ContextMap* pClientContextMap    = NULL;
        CComPtr<IWDFMemory> pMemoryIn;
        CComPtr<IWDFMemory> pMemoryOut;
        CComPtr<IWDFDevice> pDevice;
        CComPtr<IWDFFile>   pFileObject;

        //
        // Get input memory buffer, the memory object is always returned even if the
        // underlying buffer is NULL
        //
        pRequest->GetInputMemory(&pMemoryIn);
        pInputBuffer = (BYTE*) pMemoryIn->GetDataBuffer(&cbInputBuffer);

        //
        // Get output memory buffer, the memory object is always returned even if the
        // underlying buffer is NULL
        //
        pRequest->GetOutputMemory(&pMemoryOut);
        pOutputBuffer = (BYTE*) pMemoryOut->GetDataBuffer(&cbOutputBuffer);

        
        // Get the Context map for this client
        pRequest->GetFileObject(&pFileObject);
        if (pFileObject != NULL)
        {
            hr = pFileObject->RetrieveContext((void**)&pClientContextMap);
            CHECK_HR(hr, "Failed to get Contextmap from WDF File Object");
        }

        if (hr == S_OK)
        {
            // Get the device object
            pQueue->GetDevice(&pDevice );
            hr = ProcessWpdMessage(ControlCode,
                                   pClientContextMap,
                                   pDevice,
                                   pInputBuffer,
                                   (DWORD)cbInputBuffer,
                                   pOutputBuffer,
                                   (DWORD)cbOutputBuffer,
                                   &dwBytesWritten);
        }

   
    }
    else
    {
        hr = E_UNEXPECTED;
        CHECK_HR(hr, "Received invalid/unsupported IOCTL code &#39;0x%lx&#39;",ControlCode);
    }

    // Complete the request
    if (hr == S_OK)
    {
        pRequest->CompleteWithInformation(hr, dwBytesWritten);
    }
    else
    {
        pRequest->Complete(hr);
    }

    return;
}
```

**ProcessWpdMessage**方法使用验证\_WPD\_命令\_访问宏，以检查 IOCTL 和命令参数针对命令访问表定义中的开头*Queue.cpp*。

```ManagedCPlusPlus
HRESULT CQueue::ProcessWpdMessage(
    ULONG       ControlCode,
    ContextMap* pClientContextMap,
    IWDFDevice* pDevice,
    PVOID       pInBuffer,
    ULONG       ulInputBufferLength,
    PVOID       pOutBuffer,
    ULONG       ulOutputBufferLength,
    DWORD*      pdwBytesWritten)
{
    HRESULT                        hr = S_OK;
    CComPtr<IPortableDeviceValues> pParams;

    CComPtr<IPortableDeviceValues> pResults;

    CComPtr<WpdBaseDriver>         pWpdBaseDriver;

    if (hr == S_OK)
    {
        hr = m_pWpdSerializer->GetIPortableDeviceValuesFromBuffer((BYTE*)pInBuffer,
                                                                  ulInputBufferLength,
                                                                  &pParams);
        CHECK_HR(hr, "Failed to deserialize command parameters from input buffer");
    }

    // Verify that the command was sent with the appropriate access
    if (hr == S_OK)
    {
        hr = VERIFY_WPD_COMMAND_ACCESS(ControlCode, pParams, g_WpdCommandAccessMap);
        CHECK_HR(hr, "Wpd Command was sent with incorrect access flags");
    }

}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





