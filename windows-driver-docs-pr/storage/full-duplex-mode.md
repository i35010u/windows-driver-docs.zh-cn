---
title: 全双工模式
description: 全双工模式
ms.assetid: 01e3388d-d568-4476-9ff0-2125acafb841
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6f67645c7a03f4e25e5c51910e1da13453f5a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569114"
---
# <a name="full-duplex-mode"></a>全双工模式


## <span id="ddk_full_duplex_mode_kg"></span><span id="DDK_FULL_DUPLEX_MODE_KG"></span>


Storport 驱动程序支持专门为高性能总线定制的 I/O 模型。 此 I/O 模型允许在全双工模式下，这意味着微型端口驱动程序，可以对其队列中添加新请求时，即使其他人完成的过程中操作的微型端口驱动程序。 此外，在全双工模式下，微型端口驱动程序不需要同步的执行其[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)和中断服务例程。 这可能会导致显著的性能增强功能。 但是，微型端口驱动程序必须将设计为利用全双工模式下，因为 Storport 默认情况下在半双工模式下运行。

微型端口驱动程序必须配置 Storport 在全双工模式下操作执行时其[ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)例程。 这是通过初始化**SynchronizationModel**的微型端口驱动程序的成员[**端口\_配置\_信息 (STORPORT)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)结构**StorSynchronizeFullDuplex**。

 

 




