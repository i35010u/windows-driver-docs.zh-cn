---
title: 流控制
description: 流控制
ms.assetid: e7a0846e-0999-4e40-83e0-f4877871f1e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 505340af4262ec8a8d789effdc41252b8a999f83
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347325"
---
# <a name="flow-control"></a>流控制





USB 远程 NDIS 设备的流控制是 USB 规范所定义。

由于 USB 上的所有通信都基于主机到设备事务，所有主机必须执行变慢的数据流是停止到在大容量管道上设备颁发令牌中。 如果设备需要断言流控制，然后它应从主机 NAK 数据传输直到它再次便可以处理数据。 有关此过程的详细说明，请查看 USB 规范，版本 1.1 中的部分 8.4.4。

 

 





