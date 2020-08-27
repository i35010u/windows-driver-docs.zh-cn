---
description: WpdServiceSampleDriver 示例
title: WpdServiceSampleDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0ae73529253bdefcd5a9f71f531a100ccb53b1a
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969578"
---
# <a name="the-wpdservicesampledriver-sample"></a>WpdServiceSampleDriver 示例


设备服务是功能对象的扩展。 除了对设备功能进行逻辑分组以外，设备服务还提供可通过编程方式发现这些功能的应用程序。

WpdServiceSampleDriver 演示如何扩展 WpdHelloWorldDriver 示例，使其支持带有联系人设备服务的模拟设备。 通过使用此设备服务，应用程序可以发现在存储在设备上的联系人上操作的事件、方法和属性。 而且，应用程序可以使用 "联系人" 设备服务来处理这些事件，调用这些方法，或检索这些属性。 例如，应用程序可能会调用方法，将在设备上找到的联系人与计算机上存储的联系人进行同步，或者读取给定联系人的 Name 属性。

## <a name="span-idlimitationspanspan-idlimitationspanspan-idlimitationspanlimitation"></a><span id="Limitation"></span><span id="limitation"></span><span id="LIMITATION"></span>受


此驱动程序是以最简单的方式编写的，旨在演示概念。 因此，示例驱动程序可能会执行操作，或以在生产驱动程序中效率低下的方式进行结构化。 此外，此示例不使用实际硬件。 相反，它将使用内存中的数据结构来模拟设备。 因此，该驱动程序的实现方式对于生产硬件不切实际。

 

 




