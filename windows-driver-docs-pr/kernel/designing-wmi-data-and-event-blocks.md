---
title: 设计 WMI 数据和事件块
description: 设计 WMI 数据和事件块
keywords:
- WMI WDK 内核，事件块
- 事件块 WDK WMI
- 数据块 WDK WMI
- WMI WDK 内核，数据块
- 阻止 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb1d12d5e8fbb73388362513ea174c298d951679
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789799"
---
# <a name="designing-wmi-data-and-event-blocks"></a>设计 WMI 数据和事件块





为了获得更好的性能和 WMI 客户端的易用性，驱动程序应支持标准数据块，驱动程序编写者应遵循设计自定义 WMI 数据和事件块中的某些准则。 具体而言，在为数据块选择静态和动态实例名称时，驱动程序编写人员应该知道性能的折衷。 本节中的主题介绍了有关设计 WMI 数据和事件块的问题和指导原则。

 

 




