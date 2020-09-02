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
ms.openlocfilehash: b67e9295421caaf671b57a2edeec931edfd30512
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382443"
---
# <a name="nfc-polling"></a>NFC 轮询


许多 NFP 技术 (如 NFC) 必须轮询才能检测近程设备和标记的存在。 如果需要，必须以节能方式完成轮询，并且必须经常执行该操作，因为 NFP 技术显示对用户的响应能力。

### <a name="required-actions"></a>必需的措施

如果 NFP 技术必须进行轮询，则必须在硬件中执行轮询，而不会唤醒任何电脑的 Cpu，除非检测到近程设备或标记。 此外，每秒 (每 500 ms) ，轮询速率必须至少为两次。 建议的轮询速率为每秒4-5 次。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
