---
title: 处理 SRB_FUNCTION_FLUSH 和 SRB_FUNCTION_SHUTDOWN
description: 处理 SRB_FUNCTION_FLUSH 和 SRB_FUNCTION_SHUTDOWN
ms.assetid: d4b8b3e5-d895-42ca-bd28-9d3cef805654
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_FLUSH
- SRB_FUNCTION_SHUTDOWN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa6d91c8c0d98e12e41f68151bbff3b61f355e99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842333"
---
# <a name="handling-srb_function_flush-and-srb_function_shutdown"></a>处理 SRB\_函数\_FLUSH 和 SRB\_函数\_关闭


## <span id="ddk_handling_srb_function_flush_and_srb_function_shutdown_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_FLUSH_AND_SRB_FUNCTION_SHUTDOWN_KG"></span>


如果 HBA 在内部缓存数据（如[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))设置[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)），则[**HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))例程必须支持 SRB\_函数\_FLUSH 和 SRB\_函数\_关闭请求，如下所示：

-   其**function**成员设置为 SRB\_函数\_FLUSH 的 SRB 告知微型端口驱动程序将缓存在 HBA 中的数据传输到磁盘。 微型端口驱动程序必须保持刷新请求，直到传输所有缓存的数据，然后完成刷新请求。

-   当应用程序关闭文件或终止应用程序时，可能会发出此类刷新请求。

-   \_关闭，其**function**成员设置为 SRB\_函数的 SRB 告知微型端口驱动程序将数据传输到目标设备，包括刷新所有缓存的数据。 小型端口驱动程序必须保持到关闭请求，直到目标逻辑单元的 HBA 内部缓存中没有数据，然后完成关闭请求。

    请注意，可以使用多个关闭请求来调用微型端口驱动程序，该驱动程序可能针对相同的逻辑单元或针对不同逻辑单元的多个关闭请求，然后系统本身实际上会关闭。

 

 




