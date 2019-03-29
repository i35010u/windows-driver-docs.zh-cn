---
title: 关于 ISensorClassExtension
description: 关于 ISensorClassExtension
ms.assetid: 1f55f28a-796a-40e5-9995-e6a28761b9a4
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7af3c76e885cb050b4751f598fbe02ed7673105b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564474"
---
# <a name="about-isensorclassextension"></a>关于 ISensorClassExtension


传感器驱动程序将使用 ISensorClassExtension 初始化和 unitialize 传感器类扩展，引发事件，过程 WPD 输入/输出控制 (Ioctl) 代码，并正确关闭 UMDF 文件句柄。

## <a name="methods-to-manage-object-lifetime"></a>方法，用于管理对象生存期

若要初始化类扩展，基于 PnP 的硬件传感器驱动程序调用[ **ISensorClassExtension::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-initialize) UMDF 中通过调用时[ **IPnpCallbackHardware::OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)。 此步骤提供了具有指针到驱动程序的主类和实现回调接口来处理由类扩展对象引发的事件的类的类扩展对象。 该驱动程序由在 UMDF [ **IPnpCallbackHardware::OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)，则应调用[ **ISensorClassExtension::Uninitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-uninitialize) ，然后释放类扩展对象。 请注意，某些类型的传感器可能需要初始化和取消类扩展初始化在不同的时间。

## <a name="methods-to-raise-events"></a>引发事件的方法

该驱动程序可以引发各种类型的传感器事件 （通常包含传感器数据） 通过调用[ **ISensorClassExtension::PostEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)和状态信息事件，通过调用[ **ISensorClassExtension::PostStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)。 有关事件传感器驱动程序中的工作原理的详细信息，请参阅[有关传感器驱动程序事件](about-sensor-driver-events.md)。

## <a name="methods-to-manage-ioctls-and-handles"></a>方法来管理 Ioctl 和句柄

传感器驱动程序将转发至类扩展 UMDF 调用的两种类型：

-   要处理 I/O 请求控制代码通过接收[ **IQueueCallbackDeviceIoControl::OnDeviceIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)。 若要将转发至类扩展以进行处理的 I/O 请求，该驱动程序必须调用[ **ISensorClassExtension::ProcessIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-processiocontrol)。

-   有关客户端关闭通知文件通过接收的句柄[ **IFileCallbackCleanup::OnCleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)。 若要将转发 I/O 请求取消，则驱动程序必须调用[ **ISensorClassExtension::CleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-cleanupfile)。

 

 




