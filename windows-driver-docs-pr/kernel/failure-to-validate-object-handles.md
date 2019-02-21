---
title: 验证对象句柄失败
description: 验证对象句柄失败
ms.assetid: 67d52ca8-4e86-4fe2-a541-f7a0e4040b93
keywords:
- 可靠性 WDK 内核对象句柄验证
- 验证故障 WDK 内核
- 对象句柄 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 198ace4aca05664a91f8244398fe2e3bc80c6ef5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533857"
---
# <a name="failure-to-validate-object-handles"></a>验证对象句柄失败





某些驱动程序必须处理由调用方传递给它们的对象，或必须同时处理两个文件对象。 例如，调制解调器驱动程序可能会收到一个事件对象的句柄或网络驱动程序可能会收到两个不同的文件对象的句柄。 驱动程序必须验证这些句柄。 因为它们的传递由调用方，而不是通过 I/O 管理器，I/O 管理器不能执行任何验证检查。

例如，以下代码段中，驱动程序已传递的句柄**AscInfo-&gt;AddressHandle**，但还没有验证它，然后再调[ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679):

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

尽管在调用**ObReferenceObjectByHandle**成功，因此代码无法确保返回的指针引用的文件对象; 它信任调用方传入正确的信息。

即使为调用的所有参数**ObReferenceObjectByHandle**都正确，并调用成功，则驱动程序仍可以获得意外的结果，如果文件对象不适用于其驱动程序。 在以下代码片段中，驱动程序假定成功调用返回指向其预期的文件对象的指针：

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

尽管**ObReferenceObjectByHandle**返回指向文件对象，该驱动程序的指针具有不能保证该指针指向它应为文件对象。 在这种情况下，该驱动程序应访问在特定于驱动程序的数据前验证指针**AcpEndpointFileObject-&gt;FsContext**。

若要避免此类问题，驱动程序应检查有效的数据，按如下所示：

-   检查以确保它是驱动程序的预期的对象类型。

-   请确保所请求的访问是适用于的对象类型和所需的任务。 如果您的驱动程序执行快速文件复制，例如，请确保该句柄具有读取访问权限。

-   请务必指定正确的访问模式 (**UserMode**或**KernelMode**) 和访问模式适用于请求的访问权限。

-   如果该驱动程序需要的驱动程序本身创建的文件对象的句柄，验证对驱动程序的设备对象的句柄。 但是，请注意不要执行中断发送的奇怪的设备的 I/O 请求的筛选器。

-   如果您的驱动程序支持多个类型的文件对象 （如控制通道、 地址对象和 TDI 驱动程序的连接或卷、 目录和文件的文件系统的对象），请确保有一种方法来区分它们。

 

 




