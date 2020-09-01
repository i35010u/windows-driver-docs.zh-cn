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
ms.openlocfilehash: a6b6606d4b3c281904c46947a07c13c6ce8b60bb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191317"
---
# <a name="handling-srb_function_flush-and-srb_function_shutdown"></a>处理 SRB \_ 函数 \_ FLUSH 和 SRB \_ 函数 \_ 关闭


## <span id="ddk_handling_srb_function_flush_and_srb_function_shutdown_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_FLUSH_AND_SRB_FUNCTION_SHUTDOWN_KG"></span>


如果 HBA 在内部缓存数据，如 [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 设置 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)时所指示的那样， [**HwScsiStartIo**](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85)) 例程必须支持 SRB \_ 函数 \_ FLUSH 和 SRB \_ 函数 \_ SHUTDOWN 请求，如下所示：

-   其 **function** 成员设置为 SRB \_ 函数 FLUSH 的 SRB \_ 告知微型端口驱动程序将缓存在 HBA 中的数据传输到磁盘。 微型端口驱动程序必须保持刷新请求，直到传输所有缓存的数据，然后完成刷新请求。

-   当应用程序关闭文件或终止应用程序时，可能会发出此类刷新请求。

-   将其 **function** 成员设置为 SRB \_ 函数 SHUTDOWN 的 SRB \_ 告知微型端口驱动程序完成将数据传输到目标设备的功能，包括刷新所有缓存的数据。 小型端口驱动程序必须保持到关闭请求，直到目标逻辑单元的 HBA 内部缓存中没有数据，然后完成关闭请求。

    请注意，可以使用多个关闭请求来调用微型端口驱动程序，该驱动程序可能针对相同的逻辑单元或针对不同逻辑单元的多个关闭请求，然后系统本身实际上会关闭。

 

