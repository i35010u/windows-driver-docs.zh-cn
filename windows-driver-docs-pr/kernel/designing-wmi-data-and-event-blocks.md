---
title: 设计 WMI 数据和事件块
description: 设计 WMI 数据和事件块
ms.assetid: 3235accd-2bec-430e-ab00-1c5d0ef46045
keywords:
- WMI WDK 内核，事件块
- 事件阻止 WDK WMI
- 数据将阻止 WDK WMI
- WMI WDK 内核，数据块
- 块 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9562f66b1302add7a4c29fdd37367156110a343b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388183"
---
# <a name="designing-wmi-data-and-event-blocks"></a>设计 WMI 数据和事件块





为获得最佳性能和易用性的 WMI 客户端使用，驱动程序应支持标准的数据块和驱动程序编写人员应遵循特定的准则设计自定义 WMI 数据和事件块。 具体而言，驱动程序编写人员应注意的性能的权衡取舍选择静态与动态实例数据块的名称。 在本部分中的主题讨论问题和设计 WMI 数据和事件块的准则。

 

 




