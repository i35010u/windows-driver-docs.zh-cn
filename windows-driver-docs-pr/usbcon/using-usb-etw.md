---
description: 本主题提供有关活动 ID Guid 的信息、如何将这些 Guid 添加到事件跟踪提供程序中，以及如何在 Netmon 中查看它们。
title: 使用 USB ETW 跟踪中的活动 ID GUID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3290e36f9eb298a30c859e646141b6c382a87126
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716664"
---
# <a name="using-activity-id-guids-in-usb-etw-traces"></a>使用 USB ETW 跟踪中的活动 ID GUID


本主题提供有关活动 ID Guid 的信息、如何将这些 Guid 添加到事件跟踪提供程序中，以及如何在 Netmon 中查看它们。

[USB 驱动程序堆栈](usb-3-0-driver-stack-architecture.md)中的驱动程序 (2.0 和 3.0) 均为 ETW 事件跟踪提供程序。 在 Windows 7 中，从 USB 驱动程序堆栈捕获事件跟踪时，可以从其他提供程序（如其他驱动程序和应用程序）捕获跟踪。 然后，可以读取组合日志 (假设已为提供程序的事件跟踪创建了 Netmon 分析器) 。

从 Windows 8 开始，你可以通过使用 *活动 ID guid*将事件与应用程序、客户端驱动程序和 USB 驱动程序堆栈) 上的提供程序 (相关联。 当事件具有相同的活动 ID GUID 时，可以将多个提供程序中的事件与 Netmon 关联。 基于这些 Guid，Netmon 可以向你显示由上层的已检测活动导致的 USB 事件集。

在 Netmon 中查看其他提供程序的合并事件跟踪时，右键单击应用程序中的事件，然后选择 " **查找会话- &gt; NetEvent** " 以查看关联的驱动程序事件。

此图显示了应用程序、UMDF 驱动程序和 Ucx01000.sys 中的相关事件 (USB 驱动程序堆栈) 中的某个驱动程序。这些事件具有相同的活动 ID GUID。

![microsoft 网络监视器](images/netmon-activity.png)

-   [如何在应用程序中添加活动 ID GUID](#how-to-add-an-activity-id-guid-in-an-application)
-   [如何在 UMDF 驱动程序中设置活动 ID GUID](#how-to-set-the-activity-id-guid-in-a-umdf-driver)
-   [如何在内核模式驱动程序中添加活动 ID GUID](#how-to-add-activity-id-guid-in-a-kernel-mode-driver)

## <a name="how-to-add-an-activity-id-guid-in-an-application"></a>如何在应用程序中添加活动 ID GUID


应用程序可以通过调用 [**EventActivityIdControl**](/windows/win32/api/evntprov/nf-evntprov-eventactivityidcontrol)来包含活动 ID guid。 有关详细信息，请参阅 [事件跟踪函数](/windows/desktop/ETW/event-tracing-functions)。

此代码示例演示如何设置活动 ID GUID 并将其发送到 ETW 提供程序（UMDF 驱动程序）。

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

在前面的示例中，应用程序将调用 [**EventActivityIdControl**](/windows/win32/api/evntprov/nf-evntprov-eventactivityidcontrol) 来创建活动 ID (事件 \_ 活动的 \_ ctrl \_ create \_ id) ，然后将其设置为 \_ 当前线程 (事件活动 \_ ctrl \_ 设置 \_ id) 。 应用程序通过发送驱动程序定义的 IOCTL，将活动 GUID 指定到 ETW 事件提供程序，如用户模式驱动程序， (下一节) 所述。

事件提供程序必须发布检测清单文件 (。手册文件) 。 通过运行 [** ( # A0) 的消息编译器 **](/windows/desktop/WES/message-compiler--mc-exe-)，将生成包含事件提供程序、事件特性、通道和事件定义的头文件。 在此示例中，应用程序调用在生成的标头文件中定义的 EventWriteReadFail，以便在发生故障时编写跟踪事件消息。

## <a name="how-to-set-the-activity-id-guid-in-a-umdf-driver"></a>如何在 UMDF 驱动程序中设置活动 ID GUID


用户模式驱动程序通过调用 [**EventActivityIdControl**](/windows/win32/api/evntprov/nf-evntprov-eventactivityidcontrol) 创建并设置活动 ID guid，调用与应用程序调用它们的方式类似，如前一部分中所述。 这些调用将活动 ID GUID 添加到当前线程，并在线程记录事件时使用活动 ID GUID。 有关详细信息，请参阅 [使用活动标识符](../wdf/using-activity-identifiers.md)。

此示例代码演示了 UMDF 驱动程序如何设置由应用程序通过 IOCTL 创建和指定的活动 ID GUID。

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

让我们看看应用程序创建的活动 ID GUID 与 [用户模式驱动程序框架](../debugger/user-mode-driver-framework-debugging.md) （ (UMDF) 客户端驱动程序）关联的方式。 当驱动程序从应用程序接收 IOCTL 请求时，它将复制私有成员中的 GUID。 在某些时候，应用程序会调用 [**ReadFile**](/windows/win32/api/fileapi/nf-fileapi-readfile) 来执行读取操作。 框架创建请求并调用驱动程序的处理程序 ForwardFormattedRequest。 在处理程序中，驱动程序通过调用 [**EventActivityIdControl**](/windows/win32/api/evntprov/nf-evntprov-eventactivityidcontrol) 和 EventWriteReadFail 来跟踪事件消息，来在线程上设置以前存储的活动 ID GUID。

**注意**  UMDF 驱动程序还必须包含通过检测清单文件生成的标头文件。 标头文件定义编写跟踪消息的 EventWriteReadFail 的宏。



## <a name="how-to-add-activity-id-guid-in-a-kernel-mode-driver"></a>如何在内核模式驱动程序中添加活动 ID GUID


在内核模式下，驱动程序可以跟踪以用户模式或驱动程序创建的线程为的线程上的消息。 在这两种情况下，驱动程序都需要线程的活动 ID GUID。

若要跟踪消息，驱动程序必须获取注册句柄作为事件提供程序 (参阅 [**EtwRegister**](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwregister)) 然后通过指定 GUID 和事件消息来调用 [**EtwWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwwrite) 。 有关详细信息，请参阅向 [内核模式驱动程序添加事件跟踪](../devtest/adding-event-tracing-to-kernel-mode-drivers.md)。

如果内核模式驱动程序处理由应用程序或用户模式驱动程序创建的请求，则内核模式驱动程序不会创建和设置活动 ID GUID。 相反，i/o 管理器将处理大多数活动 ID 传播。 当用户模式线程启动请求时，i/o 管理器将为请求创建 IRP，并自动将当前线程的活动 ID GUID 复制到新的 IRP 中。 如果内核模式驱动程序想要跟踪该线程上的事件，则它必须通过调用 [**IoGetActivityIdIrp**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetactivityidirp)获取 GUID，然后调用 [**EtwWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwwrite)。

如果内核模式驱动程序创建一个具有活动 ID GUID 的 IRP，则驱动程序可以使用[**EtwActivityIdControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwactivityidcontrol) "事件活动" 的 " \_ \_ \_ 创建 \_ 集 ID" 来调用 EtwActivityIdControl \_ 以生成新的 GUID。 然后，该驱动程序可以通过调用 [**IoSetActivityIdIrp**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetactivityidirp)并调用 [**ETWWRITE**](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwwrite)将新 GUID 与 IRP 关联起来。

活动 ID GUID 与 IRP 一起传递到下一个较低的驱动程序。 较低版本的驱动程序可以将它们的跟踪消息添加到该线程。

## <a name="related-topics"></a>相关主题
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)