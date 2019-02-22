---
title: 启动筛选
description: 启动筛选
ms.assetid: 79ae93bc-0a6d-412a-80ca-ec4f907fb814
keywords:
- 筛选 I/O 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0323bc6d3906004828ad19b5563fd908abd29659
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521042"
---
# <a name="initiating-filtering"></a>启动筛选


## <span id="ddk_initiating_filtering_if"></span><span id="DDK_INITIATING_FILTERING_IF"></span>


在调用[ **FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305)，微筛选器驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程通常会调用[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)开始筛选 I/O 操作。

每个微筛选器驱动程序必须调用[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)从其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，以通知筛选器管理器，微筛选器驱动程序已准备好开始将附加到的卷和筛选输入/输出请求。 后面微筛选器驱动程序调用**FltStartFiltering**，筛选器管理器将微筛选器驱动程序视为完全 active 微筛选器驱动程序，向其显示 I/O 请求和通知的卷，以将附加到。 微筛选器驱动程序必须准备好开始之前接收这些 I/O 请求并通知**FltStartFiltering**返回。

MiniSpy 示例驱动程序，在[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)就，如下面的代码示例中所示：

```cpp
status = FltStartFiltering( MiniSpyData.FilterHandle );
if( !NT_SUCCESS( status )) {
  FltUnregisterFilter( MiniSpyData.FilterHandle );
}
```

如果在调用[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)不会返回状态\_微筛选器驱动程序必须调用成功后， [ **FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)来取消注册自身。

 

 




