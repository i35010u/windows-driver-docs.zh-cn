---
Description: WpdServiceSampleDriver 示例
title: WpdServiceSampleDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ade2ad76c92a80e1450c9aae73a1671e0bf5ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370488"
---
# <a name="the-wpdservicesampledriver-sample"></a>WpdServiceSampleDriver 示例


设备服务是对象的一个功能的扩展。 除了逻辑分组设备功能，设备服务提供了可以以编程方式发现这些功能的应用程序。

WpdServiceSampleDriver 演示如何扩展 WpdHelloWorldDriver 示例，以便它支持使用联系人设备服务模拟的设备。 通过使用此设备服务，应用程序可以发现事件、 方法和对存储在设备的联系人的属性。 并且，应用程序可以使用联系人设备服务能够处理这些事件，调用这些方法，或检索这些属性。 例如，应用程序可能调用的方法来同步与存储在一台计算机的联系人在设备找到的联系人或读取给定联系人名称属性。

## <a name="span-idlimitationspanspan-idlimitationspanspan-idlimitationspanlimitation"></a><span id="Limitation"></span><span id="limitation"></span><span id="LIMITATION"></span>限制


演示概念的最简单方法是编写此驱动程序。 因此，示例驱动程序可能会执行操作或效率低下到生产环境的驱动程序的方式结构化。 此外，此示例不使用实际硬件。 相反，它通过使用在内存中数据结构来模拟的设备。 因此，驱动程序可能并不现实的生产硬件的方式实现。

 

 




