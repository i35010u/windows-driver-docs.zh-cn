---
title: NFC 轮询
description: NFC 轮询
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63da1e0c78629434a100e8e188acdb08a3683fe6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812749"
---
# <a name="nfc-polling"></a>NFC 轮询


许多 NFP 技术 (如 NFC) 必须轮询才能检测近程设备和标记的存在。 如果需要，必须以节能方式完成轮询，并且必须经常执行该操作，因为 NFP 技术显示对用户的响应能力。

### <a name="required-actions"></a>必需的措施

如果 NFP 技术必须进行轮询，则必须在硬件中执行轮询，而不会唤醒任何电脑的 Cpu，除非检测到近程设备或标记。 此外，每秒 (每 500 ms) ，轮询速率必须至少为两次。 建议的轮询速率为每秒4-5 次。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
