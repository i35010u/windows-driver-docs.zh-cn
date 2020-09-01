---
title: 框架对象摘要
description: 框架对象摘要
ms.assetid: 799284a5-91c0-47b0-8f20-75a5f8e2284d
keywords:
- framework 对象 WDK KMDF，已列出
- framework 对象 WDK KMDF，摘要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a148401bba269b93f3cc55182a540f049083fe5e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190807"
---
# <a name="summary-of-framework-objects"></a>框架对象摘要


下表列出了所有框架对象并提供了有关每个对象的一些基本信息。 "模式" 列指示对象是否可用于 KMDF 和 UMDF 驱动程序，或仅用于 KMDF。

有关回调和方法以及哪些框架适用的列表，请参阅 [WDF 回调和方法摘要](/windows-hardware/drivers/ddi/_wdf/)。

|名称|Handle|目标|默认父级|驱动程序是否可以覆盖默认父级？|“模式”|参考|
|--- |--- |--- |--- |--- |--- |--- |
|子列表对象|WDFCHILDLIST|表示连接到父设备的子设备的列表。|设备对象|否|KM|[WDF 子列表对象引用](/windows-hardware/drivers/ddi/wdfchildlist/)|
|集合对象|WDFCOLLECTION|表示对象集合。|驱动程序对象|是|KM/UM|[WDF 集合对象引用](/windows-hardware/drivers/ddi/wdfcollection/)|
|通用缓冲区对象|WDFCOMMONBUFFER|表示公共缓冲区。|DMA 启用程序对象|否|KM|[WDF 公用缓冲区对象引用](/windows-hardware/drivers/ddi/wdfcommonbuffer/)|
|设备对象|WDFDEVICE|表示设备。|驱动程序对象|否|KM/UM|[WDF 设备对象引用](/windows-hardware/drivers/ddi/wdfdevice/)|
|DMA 启用程序对象|WDFDMAENABLER|允许驱动程序使用框架的 DMA 功能。|设备对象|是|KM|[WDF DMA 对象引用](/windows-hardware/drivers/ddi/wdfdmaenabler/)|
|DMA transaction 对象|WDFDMATRANSACTION|表示 DMA 事务。|DMA 启用程序对象|否|KM|[WDF DMA 对象引用](/windows-hardware/drivers/ddi/wdfdmaenabler/)|
|DPC 对象|WDFDPC|表示延迟的过程调用。|无|是|KM|[WDF DPC 对象引用](/windows-hardware/drivers/ddi/wdfdpc/)|
|驱动程序对象|WDFDRIVER|表示驱动程序。|无|否|KM/UM|[WDF 驱动程序对象引用](/windows-hardware/drivers/ddi/wdfdriver/)|
|File 对象|WDFFILEOBJECT|表示文件。|设备对象|否|KM/UM|[WDF 文件对象引用](/windows-hardware/drivers/ddi/wdffileobject/)|
|常规对象|WDFOBJECT|表示常规对象。|驱动程序对象|是|KM/UM|[WDF 常规对象引用](/windows-hardware/drivers/ddi/wdfobject/)|
|中断对象|WDFINTERRUPT|表示硬件中断资源。|设备对象|是|KM/UM|[WDF 中断对象引用](/windows-hardware/drivers/ddi/wdfinterrupt/)|
|I/o 目标对象|WDFIOTARGET|表示其他驱动程序向其发送 i/o 请求的驱动程序。|设备对象|是|KM/UM|[WDF i/o 目标对象引用](/windows-hardware/drivers/ddi/wdfiotarget/)|
|后备链表对象|WDFLOOKASIDE|表示后备链表列表。|驱动程序对象|是|KM|[WDF 内存对象引用](/windows-hardware/drivers/ddi/wdfmemory/)|
|内存对象|WDFMEMORY|表示内存缓冲区。|驱动程序对象|是|KM/UM|[WDF 内存对象引用](/windows-hardware/drivers/ddi/wdfmemory/)|
|Queue 对象|WDFQUEUE|表示接收 i/o 请求的 i/o 队列。|设备对象|是|KM/UM|[WDF 队列对象引用](/windows-hardware/drivers/ddi/wdfio/)|
|注册表项对象|WDFKEY|表示注册表项。|驱动程序对象|是|KM/UM|[WDF 注册表项对象引用](/windows-hardware/drivers/ddi/wdfregistry/)|
|请求对象|WDFREQUEST|表示 i/o 请求。|无（如果由框架创建）。 驱动程序对象（如果由驱动程序创建）。|是（如果由驱动程序创建）。|KM/UM|[WDF 请求对象引用](/windows-hardware/drivers/ddi/wdfrequest/)|
|资源列表对象|WDFCMRESLIST|表示资源列表。|驱动程序对象|否|KM/UM|[WDF 资源对象引用](/windows-hardware/drivers/ddi/wdfresource/)|
|资源范围列表对象|WDFIORESLIST|表示逻辑配置。|资源要求列表对象|否|KM|[WDF 资源对象引用](/windows-hardware/drivers/ddi/wdfresource/)|
|资源要求列表对象|WDFIORESREQLIST|表示资源需求列表。|驱动程序对象|否|KM|[WDF 资源对象引用](/windows-hardware/drivers/ddi/wdfresource/)|
|旋转锁定对象|WDFSPINLOCK|表示旋转锁。|驱动程序对象|是|KM/UM|[WDF 同步方法](/windows-hardware/drivers/ddi/wdfsync/)|
|字符串对象|WDFSTRING|表示 Unicode 字符串。|驱动程序对象|是|KM/UM|[WDF 字符串对象引用](/windows-hardware/drivers/ddi/wdfstring/)|
|Timer 对象|WDFTIMER|表示计时器。|无|是|KM/UM|[WDF 计时器对象引用](/windows-hardware/drivers/ddi/wdftimer/)|
|USB 设备对象|WDFUSBDEVICE|表示连接到 USB 的设备。|设备对象|否|KM/UM|[WDF USB 引用](/windows-hardware/drivers/ddi/wdfusb/)|
|USB 接口对象|WDFUSBINTERFACE|表示 USB 设备接口。|USB 设备对象|否|KM/UM|[WDF USB 引用](/windows-hardware/drivers/ddi/wdfusb/)|
|USB 管道对象|WDFUSBPIPE|表示 USB 设备管道。|USB 接口对象|否|KM/UM|[WDF USB 引用](/windows-hardware/drivers/ddi/wdfusb/)|
|等待-锁定对象|WDFWAITLOCK|表示等待锁。|驱动程序对象|是|KM/UM|[WDF 同步方法](/windows-hardware/drivers/ddi/wdfsync/)|
|WMI 实例对象|WDFWMIINSTANCE|表示 WMI 数据块的实例。|WMI 提供程序对象|否|KM|[WDF WMI 参考](/windows-hardware/drivers/ddi/wdfwmi/)|
|WMI 提供程序对象|WDFWMIPROVIDER|表示 WMI 数据块。|设备对象|否|KM|[WDF WMI 参考](/windows-hardware/drivers/ddi/wdfwmi/)|
|工作项对象|WDFWORKITEM|表示工作项。|无|是|KM/UM|[WDF 工作项对象引用](/windows-hardware/drivers/ddi/wdfworkitem/)|


 

 

