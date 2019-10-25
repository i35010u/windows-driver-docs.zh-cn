---
title: 编写 FilterUnloadCallback 例程
description: 编写 FilterUnloadCallback 例程
ms.assetid: 2f680770-38af-4dcb-93b8-7f770e0378b2
keywords:
- FilterUnloadCallback
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feb776ebdf29cf7ab3443d346cf0627f8863670e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840925"
---
# <a name="writing-a-filterunloadcallback-routine"></a>编写 FilterUnloadCallback 例程


## <span id="ddk_writing_a_filterunloadcallback_routine_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


*FilterUnloadCallback*例程定义如下：

```cpp
typedef NTSTATUS
(*PFLT_FILTER_UNLOAD_CALLBACK) (
    FLT_FILTER_UNLOAD_FLAGS Flags
    );
```

*FilterUnloadCallback*例程有一个输入参数*标志*，该参数可以为**NULL** ，也可以是 FLTFL\_筛选器\_卸载\_必选。 筛选器管理器将此参数设置为 FLTFL\_筛选器\_卸载\_必需，指示卸载操作是必需的。 有关此参数的详细信息，请参阅[**PFLT\_FILTER\_UNLOAD\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)。

微筛选器驱动程序的*FilterUnloadCallback*例程必须执行以下步骤：

-   关闭任何打开的内核模式通信服务器端口句柄。

-   调用[**FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)以注销微筛选器驱动程序。

-   执行任何所需的全局清除。

-   返回相应的 NTSTATUS 值。

本部分包括：

[关闭通信服务器端口](closing-the-communication-server-port.md)

[正在注销微筛选器](unregistering-the-minifilter.md)

[执行全局清除](performing-global-cleanup.md)

[从 FilterUnloadCallback 例程返回状态](returning-status-from-a-filterunloadcallback-routine.md)

 

 




