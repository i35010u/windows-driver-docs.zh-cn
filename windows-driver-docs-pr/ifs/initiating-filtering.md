---
title: 启动筛选
description: 启动筛选
keywords:
- 筛选 i/o 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89f8b7fb4c092db2d623d849d373eb275ea1622e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783245"
---
# <a name="initiating-filtering"></a>启动筛选


## <span id="ddk_initiating_filtering_if"></span><span id="DDK_INITIATING_FILTERING_IF"></span>


调用 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)后，微筛选器驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程通常会调用 [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering) 来开始筛选 i/o 操作。

每个微筛选器驱动程序都必须从其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用 [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering) ，以通知筛选器管理器：微筛选器驱动程序已准备好开始附加到卷并筛选 i/o 请求。 微筛选器驱动程序调用 **FltStartFiltering** 后，筛选器管理器会将微筛选器驱动程序视为完全活动的微身份筛选器驱动程序，并向其提供 i/o 请求和要附加到的卷的通知。 微筛选器驱动程序必须准备好在 **FltStartFiltering** 返回之前接收这些 i/o 请求和通知。

在 MiniSpy 示例驱动程序中，将调用 [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering) ，如下面的代码示例所示：

```cpp
status = FltStartFiltering( MiniSpyData.FilterHandle );
if( !NT_SUCCESS( status )) {
  FltUnregisterFilter( MiniSpyData.FilterHandle );
}
```

如果对 [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering) 的调用未返回状态 \_ SUCCESS，则微筛选器驱动程序必须调用 [**FltUnregisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter) 来取消注册。

 

