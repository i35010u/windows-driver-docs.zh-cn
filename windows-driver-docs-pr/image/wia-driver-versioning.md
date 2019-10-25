---
title: WIA 驱动程序版本控制
description: WIA 驱动程序版本控制
ms.assetid: 9ebd79ac-d742-4524-9573-5873f7a8ec37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d8fec11adbf7377eb5c717f9ae2a3b5a6c160aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840700"
---
# <a name="wia-driver-versioning"></a>WIA 驱动程序版本控制


驱动程序在从[**IStiUSD：： GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)返回的版本字段中报告它所支持的 WIA 版本（或旧版驱动程序的 STI）。 驱动程序通常将此字段设置为 STI\_版本，该版本是在*STI*中定义的。

在适用于 Windows Vista 的 Windows 驱动程序工具包（WDK）中，STI\_版本的值大于以前操作系统中 STI\_版本的值。 如果驱动程序具有 Windows Vista 的驱动程序版本值，则它必须支持 Windows Vista [IStream 数据传输](istream-data-transfers.md)。

符合新的 Windows Vista WIA 模型的 Windows Vista 驱动程序必须返回从**IStiUSD：： GetCapabilities**返回的版本字段中的 STI\_版本\_3。

 

 




