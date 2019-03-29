---
Description: This topic provides information about Activity ID GUIDs, how to add those GUIDs in the event trace providers, and view them in Netmon.
title: 使用 USB ETW 跟踪中的活动 ID GUID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8977f94f6de275cc0f47f77a2318acbf33737baf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564987"
---
# <a name="using-activity-id-guids-in-usb-etw-traces"></a>使用 USB ETW 跟踪中的活动 ID GUID


本主题介绍有关活动 ID Guid，如何添加这些 Guid 在事件跟踪提供程序，以及在网络监视器中查看它们。

中的驱动程序[USB 驱动程序堆栈](usb-3-0-driver-stack-architecture.md)（2.0 和 3.0） 是 ETW 事件跟踪提供程序。 在 Windows 7 中，同时捕获 USB 驱动程序堆栈中的事件跟踪可以捕获来自其他提供程序，例如其他驱动程序和应用程序的跟踪。 然后可以读取 （假设已创建的提供程序的事件跟踪的 Netmon 分析器） 的组合的日志。

从 Windows 8 中，您可以将关联事件提供程序 （从应用程序、 客户端驱动程序和 USB 驱动程序堆栈） 之间通过使用*活动 ID Guid*。 当事件具有相同活动 ID GUID 时，可以中 Netmon 关联来自多个提供程序的事件。 根据这些 Guid，Netmon 可显示源自在上层检测活动的 USB 事件的集。

在网络监视器中查看来自其他提供程序的组合的事件跟踪，右键单击从应用程序的事件，然后选择**找到会话-&gt; NetEvent**以查看关联驱动程序的事件。

此图显示了从应用程序、 UMDF 驱动程序和 Ucx01000.sys （USB 驱动程序堆栈中的驱动因素之一） 相关事件。这些事件具有相同活动 ID GUID。

![microsoft 网络监视器](images/netmon-activity.png)

-   [如何在应用程序中添加的活动 ID GUID](#how-to-add-an-activity-id-guid-in-an-application)
-   [如何在 UMDF 驱动程序中设置活动 ID GUID](#how-to-set-the-activity-id-guid-in-a-umdf-driver)
-   [如何将活动 ID GUID 添加到内核模式驱动程序](#how-to-add-activity-id-guid-in-a-kernel-mode-driver)

## <a name="how-to-add-an-activity-id-guid-in-an-application"></a>如何在应用程序中添加的活动 ID GUID


应用程序可以通过调用包含活动 ID Guid [ **EventActivityIdControl**](https://msdn.microsoft.com/library/windows/desktop/aa363720)。 有关详细信息，请参阅[事件跟踪函数](https://msdn.microsoft.com/library/windows/desktop/aa363795)。

此示例代码演示如何设置活动 ID GUID 并将其发送到 ETW 提供程序，UMDF 驱动程序应用程序。

```cpp
EventActivityIdControl(EVENT_ACTIVITY_CTRL_CREATE_ID, &activityIdStruct.ActivityId); 
EventActivityIdControl(EVENT_ACTIVITY_CTRL_SET_ID,    &activityIdStruct.ActivityId); 

if (!DeviceIoControl(hRead,
                     IOCTL_OSRUSBFX2_SET_ACTIVITY_ID,
                     &activityIdStruct,         // Ptr to InBuffer
                     sizeof(activityIdStruct),  // Length of InBuffer
                     NULL,                      // Ptr to OutBuffer
                     0,                         // Length of OutBuffer
                     NULL,                      // BytesReturned
                     0))                        // Ptr to Overlapped structure
{         

          wprintf(L"Failed to set activity ID - error %d\n", GetLastError());
}

...

success = ReadFile(hRead, pinBuf, G_ReadLen, (PULONG) &nBytesRead, NULL);

if(success == 0) 
{
          wprintf(L"ReadFile failed - error %d\n", GetLastError());

          EventWriteReadFail(0, GetLastError());

          ...


}
```

在前面的示例中，应用程序调用[ **EventActivityIdControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363720)若要创建的活动 ID (事件\_活动\_CTRL\_创建\_ID)，然后将其设置 (事件\_活动\_CTRL\_设置\_ID) 当前线程。 应用程序通过发送 （下一节中所述） 驱动程序定义 IOCTL 指定到 ETW 事件提供程序，如用户模式驱动程序，该活动的 GUID。

事件提供程序必须发布检测清单文件 (。MAN 文件）。 通过运行[**消息编译器 Mc.exe**](https://msdn.microsoft.com/library/windows/desktop/aa385638)，它包含定义事件提供程序、 事件属性、 通道和事件，会生成一个标头文件。 在示例中，应用程序调用 EventWriteReadFail，定义在生成的头文件中，将发生故障时的事件消息写入跟踪。

## <a name="how-to-set-the-activity-id-guid-in-a-umdf-driver"></a>如何在 UMDF 驱动程序中设置活动 ID GUID


用户模式驱动程序创建，并通过调用来设置活动 ID Guid [ **EventActivityIdControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363720)和的调用是应用程序调用它们，方式类似于上一节中所述。 这些调用添加到当前线程，并该活动 ID GUID ID GUID 每当线程记录事件时使用的活动。 有关详细信息，请参阅[使用活动标识符](https://msdn.microsoft.com/library/windows/hardware/hh706287)。

此示例代码演示如何 UMDF 驱动程序设置活动 ID GUID 时创建和指定的应用程序通过 IOCTL。

```cpp
VOID
STDMETHODCALLTYPE
CMyControlQueue::OnDeviceIoControl(
    _In_ IWDFIoQueue *FxQueue,
    _In_ IWDFIoRequest *FxRequest,
    _In_ ULONG ControlCode,
    _In_ SIZE_T InputBufferSizeInBytes,
    _In_ SIZE_T OutputBufferSizeInBytes
    )
/*++

Routine Description:


    DeviceIoControl dispatch routine

Aruments:

    FxQueue - Framework Queue instance
    FxRequest - Framework Request  instance
    ControlCode - IO Control Code
    InputBufferSizeInBytes - Lenth of input buffer
    OutputBufferSizeInBytes - Lenth of output buffer

    Always succeeds DeviceIoIoctl
Return Value:

    VOID

--*/
{
    ...

    switch (ControlCode)
    {

        ....

        case IOCTL_OSRUSBFX2_SET_ACTIVITY_ID:
        {
            if (InputBufferSizeInBytes < sizeof(UMDF_ACTIVITY_ID))
            {
                hr = HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER);
            }
            else
            {
                FxRequest->GetInputMemory(&memory );
            }

            if (SUCCEEDED(hr)) 
            {
                buffer = memory->GetDataBuffer(&bigBufferCb);
                memory->Release();

                m_Device->SetActivityId(&((PUMDF_ACTIVITY_ID)buffer)->ActivityId);
                hr = S_OK;
            }

            break;
        }
    } 
}

VOID
 SetActivityId(
        LPCGUID ActivityId
        )
    {
        CopyMemory(&m_ActivityId, ActivityId, sizeof(m_ActivityId));
    }



void
CMyReadWriteQueue::ForwardFormattedRequest(
    _In_ IWDFIoRequest*                         pRequest,
    _In_ IWDFIoTarget*                          pIoTarget
    )
{
...
    pRequest->SetCompletionCallback(
        pCompletionCallback,
        NULL
        );

...
    hrSend = pRequest->Send(pIoTarget,
                            0,  //flags
                            0); //timeout

...
    if (FAILED(hrSend))
    {
        contextHr = pRequest->RetrieveContext((void**)&pRequestContext);

        if (SUCCEEDED(contextHr)) {

            EventActivityIdControl(EVENT_ACTIVITY_CTRL_SET_ID, &pRequestContext->ActivityId);

            if (pRequestContext->RequestType == RequestTypeRead)
            {
                EventWriteReadFail(m_Device, hrSend);
            }

            delete pRequestContext;
        }

        pRequest->CompleteWithInformation(hrSend, 0);
    }

    return;
}
```

让我们看如何获取与关联的活动应用程序创建的 ID GUID[用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff560027)(UMDF) 客户端驱动程序。 当驱动程序收到 IOCTL 请求时从应用程序时，它将在私有成员中复制 GUID。 在某些时候，应用程序调用[ **ReadFile** ](https://msdn.microsoft.com/library/windows/desktop/aa365467)执行读取的操作。 框架将创建一个请求和调用驱动程序的处理程序，ForwardFormattedRequest。 在处理程序，该驱动程序的以前存储的活动 ID GUID 线程上设置通过调用[ **EventActivityIdControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363720)和 EventWriteReadFail 到跟踪事件消息。

**请注意**UMDF 驱动程序还必须包括通过检测清单文件生成的标头文件。 标头文件定义将跟踪消息写入如 EventWriteReadFail 宏。



## <a name="how-to-add-activity-id-guid-in-a-kernel-mode-driver"></a>如何将活动 ID GUID 添加到内核模式驱动程序


在内核模式驱动程序可以跟踪消息源自在用户模式下的线程或驱动程序创建的线程上。 在这两个这些情况下，驱动程序需要活动线程的 ID GUID。

跟踪消息，该驱动程序必须获取为事件提供程序的注册句柄 (请参阅[ **EtwRegister**](https://msdn.microsoft.com/library/windows/hardware/ff545603))，然后调用[ **EtwWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff545627)通过指定的 GUID 和事件消息。 有关详细信息，请参阅[添加到内核模式驱动程序的事件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff541236)。

如果您的内核模式驱动程序处理由应用程序或用户模式驱动程序创建的请求，内核模式驱动程序不创建和设置活动 ID GUID。 相反，I/O 管理器处理大部分活动 ID 传播。 当用户模式线程启动请求时，I/O 管理器创建请求 IRP，并会自动将当前线程的活动 ID GUID 复制到新的 IRP。 内核模式驱动程序而言，与该线程上的跟踪事件，它必须通过调用获取 GUID [ **IoGetActivityIdIrp**](https://msdn.microsoft.com/library/windows/hardware/hh439309)，然后调用[ **EtwWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff545627).

如果您的内核模式驱动程序与活动 ID GUID 创建 IRP，驱动程序可以调用[ **EtwActivityIdControl** ](https://msdn.microsoft.com/library/windows/hardware/ff545578)与事件\_活动\_CTRL\_创建\_设置\_ID 以生成新的 GUID。 该驱动程序中，可以然后将新的 GUID 与 IRP 的关联，通过调用[ **IoSetActivityIdIrp**](https://msdn.microsoft.com/library/windows/hardware/hh439382)，然后调用[ **EtwWrite**](https://msdn.microsoft.com/library/windows/hardware/ff545627)。

活动 ID GUID 时一起传递 IRP 到下一步的低级驱动程序。 较低的驱动程序可以将其跟踪消息添加到线程。

## <a name="related-topics"></a>相关主题
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  



