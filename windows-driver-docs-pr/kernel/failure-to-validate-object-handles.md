---
title: 无法验证对象句柄
description: 无法验证对象句柄
ms.assetid: 67d52ca8-4e86-4fe2-a541-f7a0e4040b93
keywords:
- 可靠性 WDK 内核，对象句柄验证
- 验证失败的 WDK 内核
- 对象处理 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455210e773615cb844cac4ab95a14f02d1b00bb6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189059"
---
# <a name="failure-to-validate-object-handles"></a>无法验证对象句柄





某些驱动程序必须操作由调用方传递给它们的对象，或者必须同时处理两个文件对象。 例如，调制解调器驱动程序可能会接收到事件对象的句柄，或者网络驱动程序可能会收到两个不同文件对象的句柄。 驱动程序必须验证这些句柄。 由于它们是由调用方传递的，而不是通过 i/o 管理器传递的，因此，i/o 管理器无法执行任何验证检查。

例如，在以下代码段中，驱动程序已传递 **AscInfo- &gt; AddressHandle**，但在调用 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)之前尚未对其进行验证：

```cpp
   //
   // This handle is embedded in a buffered request.
   //
   status = ObReferenceObjectByHandle(
                      AscInfo->AddressHandle,
                      0,
                      NULL,
                      KernelMode,
                      &fileObject,
                      NULL);

   if (NT_SUCCESS(status)) {
       if ( (fileObject->DeviceObject == DeviceObject) &&
            (fileObject->FsContext2 == TRANSPORT_SOCK) ) {
```

尽管对 **ObReferenceObjectByHandle** 的调用成功，但代码无法确保返回的指针引用文件对象;它信任调用方来传入正确的信息。

即使对 **ObReferenceObjectByHandle** 的调用的所有参数都是正确的，并且调用成功，如果文件对象不用于其驱动程序，驱动程序仍可能会收到意外的结果。 在下面的代码片段中，驱动程序假定成功调用返回了一个指向它所需的文件对象的指针：

```cpp
   status = ObReferenceObjectByHandle (
                             AcpInfo->Handle,
                             0L,
                             DesiredAccess,
                             *IoFileObjectType,
                             Irp->RequestorMode,
                             (PVOID *)&AcpEndpointFileObject,
                             NULL);

   if ( !NT_SUCCESS(status) ) {
      goto complete;
   }
   AcpEndpoint = AcpEndpointFileObject->FsContext;

   if ( AcpEndpoint->Type != BlockTypeEndpoint ) 
```

尽管 **ObReferenceObjectByHandle** 返回指向文件对象的指针，但驱动程序无法保证指针引用它所需的文件对象。 在这种情况下，驱动程序应在访问 **AcpEndpointFileObject- &gt; FsContext**上的特定于驱动程序的数据之前验证指针。

若要避免此类问题，驱动程序应检查是否存在有效数据，如下所示：

-   检查对象类型，确保它是驱动程序所需的类型。

-   确保请求的访问适用于对象类型和所需的任务。 例如，如果您的驱动程序执行快速文件复制，请确保该句柄具有读取访问权限。

-   请确保指定正确的访问模式 (**UserMode** 或 **KernelMode**) 并且访问模式与请求的访问权限兼容。

-   如果驱动程序需要驱动程序自身创建的文件对象的句柄，请根据设备对象或驱动程序验证该句柄。 但是，请注意不要中断发送对奇怪设备的 i/o 请求的筛选器。

-   如果你的驱动程序支持多种文件对象 (例如控制通道、地址对象和 TDI 驱动程序的连接、文件系统的卷、目录和文件对象的连接) ，请确保你有一种区分它们的方式。

 

