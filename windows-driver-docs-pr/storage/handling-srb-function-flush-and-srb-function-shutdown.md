---
title: 处理 SRB_FUNCTION_FLUSH 和 SRB_FUNCTION_SHUTDOWN
description: 处理 SRB_FUNCTION_FLUSH 和 SRB_FUNCTION_SHUTDOWN
ms.assetid: d4b8b3e5-d895-42ca-bd28-9d3cef805654
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_FLUSH
- SRB_FUNCTION_SHUTDOWN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13a329f73fa8e505d5858cf57f51337d38d2d126
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545874"
---
# <a name="handling-srbfunctionflush-and-srbfunctionshutdown"></a>处理 SRB\_函数\_刷新和 SRB\_函数\_关闭


## <span id="ddk_handling_srb_function_flush_and_srb_function_shutdown_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_FLUSH_AND_SRB_FUNCTION_SHUTDOWN_KG"></span>


如果 HBA 缓存数据在内部，指示何时[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)设置[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)，则[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)例程必须支持 SRB\_函数\_刷新和 SRB\_函数\_关闭请求，如下所示：

-   使用 SRB 及其**函数**成员设置为 SRB\_函数\_刷新指示微型端口驱动程序中的 HBA，通常为磁盘缓存的数据传输。 微型端口驱动程序必须将保存刷新请求直到所有缓存的数据已经传输和，然后，完成刷新请求。

-   当关闭文件的应用程序或终止应用程序本身时，可能产生此类刷新请求。

-   使用 SRB 及其**函数**成员设置为 SRB\_函数\_关闭指示微型端口驱动程序完成传输数据，包括所有缓存的数据，刷新到目标设备。 微型端口驱动程序都必须将保存关闭请求直到 HBA 的内部缓存中没有数据将保留目标逻辑单元，并完成关闭请求，然后。

    请注意，微型端口驱动程序可以调用使用多个关闭请求，可能是因为在同一逻辑单元或使用多个关闭请求，不同的逻辑单元，系统本身实际上关闭之前。

 

 




