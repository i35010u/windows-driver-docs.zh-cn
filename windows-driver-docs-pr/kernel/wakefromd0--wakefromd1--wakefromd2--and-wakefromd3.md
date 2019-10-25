---
title: WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3
description: WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3
ms.assetid: f01aaceb-babf-42da-bc4b-1a846c84a313
keywords:
- WakeFromD0
- WakeFromD1
- WakeFromD2
- WakeFromD3
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d6015f4d0a6c63754b1dabbe2b5256ba01700ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835772"
---
# <a name="wakefromd0-wakefromd1-wakefromd2-and-wakefromd3"></a>WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3





其中每个[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构成员指示设备是否可以唤醒，以响应在设备处于指定状态时到达的外部信号。

对于支持所有四种设备电源状态的设备（D0、D1、D2、D3），但只能从状态 D0 和 D1 唤醒，并设置**WakeFromD0**和**WakeFromD1**位，并且**WakeFromD2**和**WakeFromD3**位清晰。

 

 




