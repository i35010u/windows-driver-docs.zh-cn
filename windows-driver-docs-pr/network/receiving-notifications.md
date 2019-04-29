---
title: 接收通知
description: 接收通知
ms.assetid: 852243b2-35b0-4c94-9b3b-9855ed1a678a
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa03f6d5fa841fd7c0e7efc8d616cf2069e1f147
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380575"
---
# <a name="receiving-notifications"></a>接收通知




 

操作系统将通过调用转发从本机 802.11 微型端口驱动程序的特定于 IHV 的迹象[ *Dot11ExtIhvReceiveIndication* ](https://msdn.microsoft.com/library/windows/hardware/ff547512)函数。 有关如何驱动程序将指示此类型的详细信息，请参阅[IHV 特定指示](ihv-specific-indications.md)。

当[ *Dot11ExtIhvReceiveIndication* ](https://msdn.microsoft.com/library/windows/hardware/ff547512)调用函数时， *pvBuffer*参数传递给包含 IHV 定义的格式中的数据的缓冲区的指针。

 

 





