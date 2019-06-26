---
title: WIA 驱动程序版本控制
description: WIA 驱动程序版本控制
ms.assetid: 9ebd79ac-d742-4524-9573-5873f7a8ec37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53fdbbdfff36c90bdfb2794f7dea1db27c9653f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365007"
---
# <a name="wia-driver-versioning"></a>WIA 驱动程序版本控制


驱动程序报告的版本 WIA （或 STI 旧驱动程序），它支持从返回的版本字段[ **IStiUSD::GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getcapabilities)。 驱动程序通常将此字段设置为 STI\_版本中定义*Sti.h*。

适用于 Windows Vista，STI 的值在 Windows 驱动程序工具包 (WDK)\_版本高于 STI 值\_中早期版本的操作系统版本。 如果驱动程序包含其驱动程序版本的 Windows Vista 值，则它必须支持 Windows Vista [IStream 数据传输](istream-data-transfers.md)。

遵循新的 Windows Vista WIA 模型的 Windows Vista 驱动程序必须返回 STI\_版本\_从返回的版本字段中的 3 **IStiUSD::GetCapabilities**。

 

 




