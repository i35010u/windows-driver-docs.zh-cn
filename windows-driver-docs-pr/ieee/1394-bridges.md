---
title: 1394 桥
description: 1394 桥
keywords:
- IEEE 1394 WDK 总线，网桥
- 1394 WDK 总线，网桥
- 桥接 WDK IEEE 1394 总线
- 1394桥接器 IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b8bce8e0946da5b498d2424c17f77cdb9319b16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794967"
---
# <a name="1394-bridges"></a>1394 桥





1394基本堆栈 (*ohci1394.sys* 和 *1394bus.sys*) 不支持 1394 bridge 设备，也不支持多个1394总线之间的桥接。 这是因为，1394基本堆栈不允许多个总线号。 它将总线号0x3FF 用于所有总线操作。 这是由 IEEE 1394-1995 规范定义的本地总线号码的协议标准。

由于桥要求操作系统支持多个总线编号才能正常运行，因此 Microsoft 不保证附加到桥的1394设备将正常运行。

 

 




