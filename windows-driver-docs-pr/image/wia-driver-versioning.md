---
title: WIA 驱动程序版本控制
description: WIA 驱动程序版本控制
ms.assetid: 9ebd79ac-d742-4524-9573-5873f7a8ec37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd3f78b7f93b2535f968c62b004b546317ce6e94
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185011"
---
# <a name="wia-driver-versioning"></a>WIA 驱动程序版本控制


驱动程序会在从 [**IStiUSD：： GetCapabilities**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)返回的版本字段中报告 (的 WIA 版本或 STI) 的版本。 驱动程序通常将此字段设置为 \_ 在 *STI*中定义的 STI 版本。

在 windows STI 的 Windows 驱动程序)  (工具包中，Windows Vista 的 \_ 版本值大于 \_ 以前操作系统中 STI 版本的值。 如果驱动程序具有 Windows Vista 的驱动程序版本值，则它必须支持 Windows Vista [IStream 数据传输](istream-data-transfers.md)。

符合新的 Windows Vista WIA 模型的 Windows Vista 驱动程序必须返回 \_ \_ 从 **IStiUSD：： GetCapabilities**返回的版本字段中的 STI 版本3。

 

