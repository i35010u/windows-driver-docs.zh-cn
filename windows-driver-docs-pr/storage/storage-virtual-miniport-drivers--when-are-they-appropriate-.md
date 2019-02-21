---
title: 存储虚拟微型端口驱动程序时是否合适
description: 存储虚拟微型端口驱动程序时是否合适
ms.assetid: 45b9eab9-15b8-4244-bd16-e8850211b8bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 184525d984acba8f2a99f1773b7adf0fb161c1c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542057"
---
# <a name="storage-virtual-miniport-drivers-when-are-they-appropriate"></a>存储虚拟微型端口驱动程序：何时是否合适？


虚拟微型端口驱动程序适合，它完全模拟一个或多个设备，或它不具有自己的控制的任何硬件，但它与另一台设备使用设备的驱动程序作为传输的 I/O 请求。 例如，使用随机存取内存 (RAM) 来存储其数据的磁盘设备通常称为 RAMDISK。 这是不当使用虚拟微型端口驱动程序的一个很好示例。 另一个示例就是提供一个用于发送和接收存储命令和数据的通信链接的网络适配器的某种类型的使用。 网络适配器具有其自己控制其硬件的设备驱动程序，但只与该驱动程序，并不是基础硬件的虚拟微型端口通信。

当它直接控制实际硬件，例如，主机总线适配器时，不适合虚拟微型端口。

 

 




