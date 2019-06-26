---
title: 启动筛选
description: 启动筛选
ms.assetid: 79ae93bc-0a6d-412a-80ca-ec4f907fb814
keywords:
- 筛选 I/O 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90083473c6739f62168313d09df8a50b6189d2dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381741"
---
# <a name="initiating-filtering"></a>启动筛选


## <span id="ddk_initiating_filtering_if"></span><span id="DDK_INITIATING_FILTERING_IF"></span>


在调用[ **FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)，微筛选器驱动程序[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程通常会调用[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)开始筛选 I/O 操作。

每个微筛选器驱动程序必须调用[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)从其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程，以通知筛选器管理器，微筛选器驱动程序已准备好开始将附加到的卷和筛选输入/输出请求。 后面微筛选器驱动程序调用**FltStartFiltering**，筛选器管理器将微筛选器驱动程序视为完全 active 微筛选器驱动程序，向其显示 I/O 请求和通知的卷，以将附加到。 微筛选器驱动程序必须准备好开始之前接收这些 I/O 请求并通知**FltStartFiltering**返回。

MiniSpy 示例驱动程序，在[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)就，如下面的代码示例中所示：

```cpp
status = FltStartFiltering( MiniSpyData.FilterHandle );
if( !NT_SUCCESS( status )) {
  FltUnregisterFilter( MiniSpyData.FilterHandle );
}
```

如果在调用[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)不会返回状态\_微筛选器驱动程序必须调用成功后， [ **FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltunregisterfilter)来取消注册自身。

 

 




