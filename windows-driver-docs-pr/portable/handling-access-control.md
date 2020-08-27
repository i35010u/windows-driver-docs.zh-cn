---
description: 处理访问控制
title: 处理访问控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d4e1d8281e4e398884e8990091f7f1e2ca732c4
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968804"
---
# <a name="handling-access-control"></a>处理访问控制


WPD 驱动程序必须验证 WPD 命令负载是否与正确的 i/o 控制代码 (IOCTL) 一起发送，以确保 i/o 管理器执行了相应的 ACL 检查。 由于每个驱动程序都必须执行此验证，因此 WPD 会提供宏来自动执行此过程。

这些宏在文件 *PortableDevice*中定义。 下表对它们进行了说明。

| 宏                                            | 描述                                                                                                                                  |
|--------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| BEGIN \_ WPD \_ 命令 \_ 访问 \_ 映射                 | 定义命令访问表的开头。                                                                                           |
| DECLARE \_ VERIFY \_ WPD \_ 命令 \_ 访问            | 声明函数的实例，该函数用于验证是否随 IOCTL 中的相应访问标志一起发送了给定的 WPD 命令。 |
| 声明 \_ WPD \_ 标准 \_ 命令 \_ 访问 \_ 项 | 声明 *PortableDevice*中包含的所有标准 WPD 命令的条目。                                                 |
| 结束 \_ WPD \_ 命令 \_ 访问 \_ 映射                   | 定义命令访问表的末尾。                                                                                                 |
| 是 \_ WPD \_ IOCTL                                   | 确定给定的 IOCTL 是否特定于 WPD。                                                                                         |
| 验证 \_ WPD \_ 命令 \_ 访问                     | 将给定的 IOCTL 及其参数与某个驱动程序模块中定义的命令访问表进行比较。                     |
| WPD \_ 命令 \_ 访问 \_ 项                      | 向命令访问表中添加一个自定义项。                                                                                             |

 

在示例驱动程序中，访问控制验证在 **CQueue：： OnDeviceIoControl** 和 **CQueue：:P rocesswpdmessage** 方法中执行。 这些方法位于 *队列 .cpp* 文件中。 此外，此文件还包含一个命令访问表，其中列出了 WPD 以及任何自定义 IOCTLs 及其访问级别。

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

**OnDeviceIoControl**方法使用 IS \_ WPD \_ IOCTL 宏来识别 WPD IOCTLs，然后通过调用**ProcessWpdMessage**方法对其进行处理。

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
        CHECK_HR(hr, "Received invalid/unsupported IOCTL code '0x%lx'",ControlCode);
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

**ProcessWpdMessage**方法使用 VERIFY \_ WPD \_ 命令 \_ 访问宏来对照在*Queue*开头定义的命令访问表检查 IOCTL 和命令参数。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





