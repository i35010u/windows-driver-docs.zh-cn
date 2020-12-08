---
title: 适用时的存储虚拟微型端口驱动程序
description: 适用时的存储虚拟微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1642da1662eae1a4ecf178c1b3d8db019deca1bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834971"
---
# <a name="storage-virtual-miniport-drivers-when-are-they-appropriate"></a>存储虚拟微型端口驱动程序：何时适合？


虚拟微型端口驱动程序适用于完全模拟一个或多个设备，或者它没有自己的硬件来控制，但会使用其设备驱动程序作为 i/o 请求的传输方式与其他设备通信。 例如，使用随机存取内存 (RAM) 存储其数据的磁盘设备通常称为 RAMDISK。 这是适当使用虚拟微型端口驱动程序的一个好示例。 另一个示例是使用某种类型的网络适配器，该适配器提供用于发送和接收存储命令和数据的通信链接。 网络适配器具有其自己的设备驱动程序，可控制其硬件，但虚拟微型端口仅与驱动程序通信，而不与基础硬件通信。

如果虚拟小型端口直接控制实际硬件（例如，主机总线适配器），则它不适合。

 

 




