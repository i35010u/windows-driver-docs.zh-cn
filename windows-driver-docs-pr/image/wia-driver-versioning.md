---
title: WIA 驱动程序版本控制
description: WIA 驱动程序版本控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652ca31896c7ef7f2929399aa27bdfb7b0c1be2c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820235"
---
# <a name="wia-driver-versioning"></a>WIA 驱动程序版本控制


驱动程序会在从 [**IStiUSD：： GetCapabilities**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)返回的版本字段中报告 (的 WIA 版本或 STI) 的版本。 驱动程序通常将此字段设置为 \_ 在 *STI* 中定义的 STI 版本。

在 windows STI 的 Windows 驱动程序)  (工具包中，Windows Vista 的 \_ 版本值大于 \_ 以前操作系统中 STI 版本的值。 如果驱动程序具有 Windows Vista 的驱动程序版本值，则它必须支持 Windows Vista [IStream 数据传输](istream-data-transfers.md)。

符合新的 Windows Vista WIA 模型的 Windows Vista 驱动程序必须返回 \_ \_ 从 **IStiUSD：： GetCapabilities** 返回的版本字段中的 STI 版本3。

 

