---
title: KSINTERFACESETID \_ 标准
description: KSINTERFACESETID \_ 标准
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c3b98a1cffa91bc70d7ea45273cd415425d76e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790209"
---
# <a name="ksinterfacesetid_standard"></a>KSINTERFACESETID \_ 标准


## <span id="ddk_ksinterfacesetid_standard_ks"></span><span id="DDK_KSINTERFACESETID_STANDARD_KS"></span>


此接口集包含各种 pin 可支持的常规接口类型。 若要了解如何指定你的 pin 类型支持的接口，请参阅 [KS 接口](./ks-interfaces.md)。

对于内存描述符列表 (MDL) 的流式处理，请求的发起方必须为列表中的每个 MDL 创建流标头，并在 IRP 完成后，如果无法释放 MDL 列表，则分配一个完成例程。

KSINTERFACESETID 标准集中的以下接口类型 \_ 在 KSINTERFACE standard 中枚举 \_ ：

[**KSINTERFACE \_ 标准 \_ 流式处理**](ksinterface-standard-streaming.md)

[**KSINTERFACE \_ 标准 \_ 循环 \_ 流式处理**](ksinterface-standard-looped-streaming.md)

[**KSINTERFACE \_ 标准 \_ 控件**](ksinterface-standard-control.md)

 

