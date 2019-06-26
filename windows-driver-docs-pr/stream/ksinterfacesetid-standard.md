---
title: KSINTERFACESETID\_标准
description: KSINTERFACESETID\_标准
ms.assetid: f921ffba-04dd-4900-8825-5b3486009bca
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 017fab5840becdadbc565974950a23d4e806d207
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370424"
---
# <a name="ksinterfacesetidstandard"></a>KSINTERFACESETID\_标准


## <span id="ddk_ksinterfacesetid_standard_ks"></span><span id="DDK_KSINTERFACESETID_STANDARD_KS"></span>


此接口集包含各种 pin 可以支持的常规接口类型。 若要了解如何指定你的 pin 类型支持哪些界面，请参阅[KS 接口](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-interfaces)。

有关内存描述符列表 (MDL) 的基于流式处理，请求的发起方必须为在列表中，每个 MDL 创建流标头，并分配完成例程，如果 MDL 列表必须不会释放 IRP 完成。

以下接口类型中 KSINTERFACESETID\_KSINTERFACE 中列举了标准集\_标准：

[**KSINTERFACE\_STANDARD\_STREAMING**](ksinterface-standard-streaming.md)

[**KSINTERFACE\_标准\_LOOPED\_流式处理**](ksinterface-standard-looped-streaming.md)

[**KSINTERFACE\_标准\_控件**](ksinterface-standard-control.md)

 

 





