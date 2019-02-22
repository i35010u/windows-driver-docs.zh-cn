---
title: 1394 桥
description: 1394 桥
ms.assetid: 208cceaa-dd26-46f9-b015-723c5940b02b
keywords:
- IEEE 1394 WDK 总线桥
- 1394 WDK 总线桥
- 桥 WDK IEEE 1394 总线
- 1394 桥 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8486fb5725f43b19db5761816d8b6be6f2947942
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522509"
---
# <a name="1394-bridges"></a>1394 桥





1394 基堆栈 (*ohci1394.sys*并*1394bus.sys*) 不支持 1394年桥接设备或多个 1394年总线之间的桥接。 这是因为 1394年基堆栈不允许多个总线编号。 它使用总线数 0x3FF 总线的所有操作。 这是本地总线数字议定的标准由 IEEE 1394 1995年规范定义。

由于桥需要的操作系统支持多个总线编号才能正常运行，Microsoft 不保证 1394年附加到桥的设备将继续工作。

 

 




