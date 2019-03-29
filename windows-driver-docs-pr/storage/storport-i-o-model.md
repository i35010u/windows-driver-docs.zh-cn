---
title: Storport I/O 模型
description: Storport I/O 模型
ms.assetid: 9220b01e-725f-4a03-87f1-402c0686cccd
keywords:
- Storport 驱动程序 WDK I/O
- I/O WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07360d804cf18580db8865f880fc966c44ffe261
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568418"
---
# <a name="storport-io-model"></a>Storport I/O 模型


## <span id="ddk_storport_i_o_model_kg"></span><span id="DDK_STORPORT_I_O_MODEL_KG"></span>


本部分介绍 Storport 驱动程序的 I/O 模型并对此模型中使用的 SCSI 端口驱动程序进行了对比。 Storport I/O 模型包含多个功能旨在使性能最充分地利用潜在的高速总线和存储设备。

Storport 驱动程序使用推送模型的 I/O。 这意味着该驱动程序将以异步方式对其微型端口驱动程序，最大数量的重叠数据包的 I/O 请求转发而无需等待微型端口驱动程序请求的输入。 在推送模型中，端口驱动程序控制的 I/O 请求流，并将推送到微型端口驱动程序的请求。

另一方面，SCSI 端口驱动程序使用 I/O 请求的模型。 在请求模型中的 I/O，SCSI 端口驱动程序以同步方式将转发到其微型端口驱动程序的 I/O 请求并等待微型端口驱动程序，以请求新的输入，再发送下一步的 I/O 请求。 此外，微型端口驱动程序控制的 I/O 请求流和端口驱动程序中向下拉取请求。

SCSI 端口驱动程序的 I/O 模型的详细信息，请参阅[SCSI 端口 I/O 模型](scsi-port-i-o-model.md)。

在本部分中所涉及的主题如下所示：

[Full-Duplex Mode](full-duplex-mode.md)

[半双工模式：不适合于已发布产品](half-duplex-mode--not-appropriate-for-shipped-products.md)

[未同步的 HwStorBuildIo 例程](unsynchronized-hwstorbuildio-routine.md)

[未同步的微型端口驱动程序例程中的同步的访问](synchronized-access-within-unsynchronized-miniport-driver-routines.md)

[访问 Storport I/O 模型中的分散/收集列表](access-to-scatter-gather-lists-in-the-storport-i-o-model.md)

[Storport I/O 模型中的映射缓冲区的使用](use-of-mapping-buffers-in-the-storport-i-o-model.md)

[性能提示：在 HwStartIo 期间完成的请求](performance-tip--completing-requests-during-hwstartio.md)

[预处理和后处理的 Cdb 和探测代码](pre--and-post-processing-of-cdbs-and-sense-codes.md)

 

 




