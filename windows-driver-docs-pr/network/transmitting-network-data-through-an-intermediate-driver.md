---
title: 通过中间驱动程序传输网络数据
description: 通过中间驱动程序传输网络数据
ms.assetid: 90759322-810b-47fd-896c-465c96be4cdd
keywords:
- 中间驱动程序 WDK 网络传输数据
- NDIS 中间层驱动程序 WDK，传输数据
- 将网络数据传输
- 数据传输 WDK NDIS 中间
- 将 WDK NDIS 中间数据传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d82c2602edf324facab2918faf05ff0444cb87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569462"
---
# <a name="transmitting-network-data-through-an-intermediate-driver"></a>通过中间驱动程序传输网络数据





如中所述[微型端口驱动程序作为注册 Intermediate Driver](registering-an-intermediate-driver-as-a-miniport-driver.md)，中间驱动程序必须提供[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)函数时它使用注册[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)。 *MiniportSendNetBufferLists*函数可以转发传入[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构通过调用[**NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)如果驱动程序有无连接的下边缘。 *MiniportSendNetBufferLists*可以发送的 NET 列表\_缓冲区\_收到与列表结构**NdisSendNetBufferLists**而不考虑基础微型端口的功能驱动程序。

*MiniportSendNetBufferLists*接收的 NET 列表\_缓冲区\_由基础调用方的顺序排列的列表结构**NdisSendNetBufferLists**。 在大多数情况下，中间驱动程序应维护此顺序传递数组传入 NET\_缓冲区\_列表结构到基础微型端口驱动程序。 传递到基础驱动程序之前，修改网络数据中的数据的中间驱动程序可以对列表重新排序。

NDIS 始终保留的顺序[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构指针传递到链接列表作为**NdisSendNetBufferLists**. 基础的微型端口驱动程序还假定在传递到该列表及其*MiniportSendNetBufferLists*函数意味着网络数据应传输相同的顺序。

 

 





