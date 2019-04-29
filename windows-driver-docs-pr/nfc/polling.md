---
title: NFC 轮询
description: NFC 轮询
ms.assetid: C6C531EC-59AA-4AF5-903E-A726C0E79E47
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d099d6b189ef9cdc618df03eab1fdf48da3798ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373711"
---
# <a name="nfc-polling"></a>NFC 轮询


许多 NFP 技术 （如 NFC) 必须轮询来检测近程设备和标记的状态。 时必需的轮询必须进行 power 高效的方式，并且必须完成通常足够的 NFP 技术将显示对用户的响应能力。

### <a name="required-actions"></a>所需的操作

如果必须轮询 NFP 技术，您必须轮询的完成硬件中而无需任何 PC 的 Cpu 唤醒，除非检测到近程设备或标记。 此外，轮询速率必须每秒 (每 500 ms) 在至少两次。 建议的轮询速率为每秒 4 到 5 倍。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
 

