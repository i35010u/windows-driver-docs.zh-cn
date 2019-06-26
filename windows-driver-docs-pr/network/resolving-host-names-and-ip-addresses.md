---
title: 解析主机名和 IP 地址
description: 解析主机名和 IP 地址
ms.assetid: 4a5f421c-6827-4ca2-be88-67ec43dc84b2
keywords:
- WSK WDK 网络、 名称解析
- 网络、 Winsock 内核 WDK 名称解析
- 主机名称转换到传输地址 WDK Winsock 内核
- 为主机名 WDK Winsock 内核的传输地址转换
- 传输地址 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a28d1ca7dc86a575658eec00125f8a0bfd2df826
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378648"
---
# <a name="resolving-host-names-and-ip-addresses"></a>解析主机名和 IP 地址


从 Windows 7 开始*内核的名称解析*功能允许内核模式组件来执行之间 Unicode 主机名和传输地址的独立于协议的转换。 可以使用以下[Winsock Kernel (WSK)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)客户端级别的功能来执行此名称解析：

-   [**WskFreeAddressInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_free_address_info)

-   [**WskGetAddressInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_get_address_info)

-   [**WskGetNameInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_get_name_info)

这些函数执行类似于用户模式下函数的名称地址转换[ **FreeAddrInfoW**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-freeaddrinfow)， [ **GetAddrInfoW**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-getaddrinfow)，并[ **GetNameInfoW**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-getnameinfow)分别。

若要充分利用此功能，必须编译或重新编译您的驱动程序与 NTDDI\_版本宏设置为 NTDDI\_WIN7 或更高版本。

为了使您的驱动程序使用内核名称解析功能，它必须执行以下调用顺序：

1.  调用[ **WskRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskregister) WSK 向注册。

2.  调用[ **WskCaptureProviderNPI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskcaptureprovidernpi)捕获 WSK 提供程序[网络编程接口 (NPI)](network-programming-interface.md)。

3.  完成后使用 WSK 提供程序 NPI，调用[ **WskReleaseProviderNPI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskreleaseprovidernpi) WSK 提供程序 NPI 发布。

4.  调用[ **WskDeregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskderegister)能够取消注册 WSK 应用程序。

下面的代码示例使用上面的调用顺序来显示如何调用 WSK 应用程序**WskGetAddressInfo**函数转换的传输地址将主机名。

```C++
NTSTATUS
SyncIrpCompletionRoutine(
    __in PDEVICE_OBJECT Reserved,
    __in PIRP Irp,
    __in PVOID Context
    )
{    
    PKEVENT compEvent = (PKEVENT)Context;
    UNREFERENCED_PARAMETER(Reserved);
    UNREFERENCED_PARAMETER(Irp);
    KeSetEvent(compEvent, 2, FALSE);    
    return STATUS_MORE_PROCESSING_REQUIRED;
}

NTSTATUS
KernelNameResolutionSample(
    __in PCWSTR NodeName,
    __in_opt PCWSTR ServiceName,
    __in_opt PADDRINFOEXW Hints,
    __in PWSK_PROVIDER_NPI WskProviderNpi
    )
{
    NTSTATUS status;
    PIRP irp;
    KEVENT completionEvent;
    UNICODE_STRING uniNodeName, uniServiceName, *uniServiceNamePtr;
    PADDRINFOEXW results;

    PAGED_CODE();
    //
    // Initialize UNICODE_STRING structures for NodeName and ServiceName 
    //
 
    RtlInitUnicodeString(&uniNodeName, NodeName);

    if(ServiceName == NULL) {
        uniServiceNamePtr = NULL;
    }
    else {
        RtlInitUnicodeString(&uniServiceName, ServiceName);
        uniServiceNamePtr = &uniServiceName;
    }

    //
    // Use an event object to synchronously wait for the 
    // WskGetAddressInfo request to be completed. 
    //
 
    KeInitializeEvent(&completionEvent, SynchronizationEvent, FALSE);

    //
    // Allocate an IRP for the WskGetAddressInfo request, and set the 
    // IRP completion routine, which will signal the completionEvent
    // when the request is completed.
    //
 
    irp = IoAllocateIrp(1, FALSE);
    if(irp == NULL) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }        

    IoSetCompletionRoutine(irp, SyncIrpCompletionRoutine, 
  &completionEvent, TRUE, TRUE, TRUE);

    //
    // Make the WskGetAddressInfo request.
    //
 
    WskProviderNpi->Dispatch->WskGetAddressInfo (
        WskProviderNpi->Client,
        &uniNodeName,
        uniServiceNamePtr,
        NS_ALL,
        NULL, // Provider
        Hints,
        &results, 
        NULL, // OwningProcess
        NULL, // OwningThread
        irp);

    //
    // Wait for completion. Note that processing of name resolution results
    // can also be handled directly within the IRP completion routine, but
    // for simplicity, this example shows how to wait synchronously for 
    // completion.
    //
 
    KeWaitForSingleObject(&completionEvent, Executive, 
                        KernelMode, FALSE, NULL);

    status = irp->IoStatus.Status;

    IoFreeIrp(irp);

    if(!NT_SUCCESS(status)) {
        return status;
    }

    //
    // Process the name resolution results by iterating through the addresses
    // within the returned ADDRINFOEXW structure.
    //
 
   results; // your code here

    //
    // Release the returned ADDRINFOEXW structure when no longer needed.
    //
 
    WskProviderNpi->Dispatch->WskFreeAddressInfo(
        WskProviderNpi->Client,
        results);

    return status;
} 
```

 

 





