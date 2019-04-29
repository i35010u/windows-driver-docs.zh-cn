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
ms.openlocfilehash: 5c4b5d45df5e3e6e150c449464b51698fc07584f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391441"
---
# <a name="wakefromd0-wakefromd1-wakefromd2-and-wakefromd3"></a>WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3





每种[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构成员指示设备是否可以被唤醒以响应到达时在设备处于指定状态的外部信号。

支持所有四个设备电源的设备状态 D0、 D1、 D2 （D3） 但可仅从状态 D0 和 D1，唤醒**WakeFromD0**并**WakeFromD1**位将设置，和**WakeFromD2**并**WakeFromD3**位都被清除。

 

 




