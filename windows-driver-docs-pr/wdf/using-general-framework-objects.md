---
title: 使用常规框架对象
description: 使用常规框架对象
ms.assetid: d3356d3f-8110-44dd-b4a2-36265f5a1714
keywords:
- framework 对象 WDK KMDF，常规
- 常规框架对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8c2c310b79638b54f20b99ed77456e1af7b29e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843078"
---
# <a name="using-general-framework-objects"></a>使用常规框架对象


*常规框架对象*是框架对象，其他所有类型的框架对象均派生自该对象。

与其他框架对象一样，常规对象支持引用计数、上下文空间、删除回调函数和父对象，如[框架对象简介](introduction-to-framework-objects.md)中所述。

驱动程序可以创建和使用常规框架对象。 如果驱动程序调用[**WdfObjectCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectcreate)来创建常规对象，则驱动程序可以：

-   为每个常规对象创建一个或多个上下文空间。

    您可以使用对象上下文空间来存储要与常规对象关联的系统资源的相关信息。

    有关上下文空间的详细信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

-   为常规对象分配父级。

    删除父对象时，将删除常规对象。 例如，如果您的驱动程序将框架设备对象指定为其某个常规对象的父对象，则该框架将在删除该设备对象时删除该常规对象。

    驱动程序通过将对象的[**WDF\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)的**ParentObject**成员设置\_属性结构来指定对象的父对象。

-   提供删除回调函数。

    驱动程序可以提供[*EvtCleanupCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)和[*EvtDestroyCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)函数，该函数可释放在创建常规对象时，驱动程序分配的系统资源。 例如，如果驱动程序在创建常规对象时调用了[**ExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool) ，则清理或销毁回调函数可以调用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)。

使用常规对象可以方便地管理驱动程序分配的资源。 例如，如果驱动程序将请求发送到多个设备，或将请求分成几个较小的请求，则较高级别的驱动程序可能需要多个内存分配来处理收到的 i/o 请求。 驱动程序可以创建一个或多个作为接收到的 i/o 请求的子级的常规对象，并可以在常规对象的上下文空间中存储有关内存分配的信息。

 

 





