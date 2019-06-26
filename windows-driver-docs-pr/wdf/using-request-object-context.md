---
title: 使用请求对象上下文
description: 使用请求对象上下文
ms.assetid: befb4a22-0640-45e3-890e-6ff17969b017
keywords:
- 请求对象 WDK KMDF，上下文空间
- 上下文空间 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a70ef85a9c1de9119e7e7ec5f405ce0e9149bfbf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372215"
---
# <a name="using-request-object-context"></a>使用请求对象上下文





每个框架请求对象，由框架还是由驱动程序，创建可以包含驱动程序定义的上下文的空间。 基于框架的驱动程序初始化时 framework 设备对象，该驱动程序可以调用[ **WdfDeviceInitSetRequestAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)若要指定[ **WDF\_对象\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)描述设备的请求对象的上下文空间的结构。

该框架，如下所示分配的请求对象的上下文空间：

-   当 framework 创建您的驱动程序的请求对象时，它会分配上下文空间使用它的调用时，您的驱动程序指定的大小**WdfDeviceInitSetRequestAttributes**。

-   如果您的驱动程序通过调用创建额外的请求对象[ **WdfRequestCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)，可以通过提供 WDF 指定上下文大小\_对象\_属性结构。

有关分配和访问 framework 对象的上下文空间的详细信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

 

 





