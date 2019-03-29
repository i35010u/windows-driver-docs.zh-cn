---
title: 在 AVStream 编解码器中使用硬件媒体
description: 在 AVStream 编解码器中使用硬件媒体
ms.assetid: 07c25875-c549-4d47-ac0d-605f2aa9daa4
keywords:
- AVStream 硬件编解码器支持 WDK，使用硬件媒体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e244540a8f89636a248eee17e6366966a6fe0dbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565677"
---
# <a name="using-hardware-mediums-in-avstream-codecs"></a>在 AVStream 编解码器中使用硬件媒体


AVStream 微型驱动程序支持专用介质可将设备硬件，而无需中间传输到系统内存中的数据传输。

具体而言，如果两个筛选器共享相同的专用中等和中型实例，媒体基础传输以独占方式中的设备硬件的媒体。 此传输时将不会引入的系统内存的函数。 例如，解码器和编码器在同一设备可以共享一个专用的媒介，这会导致显著改进了性能。

若要使用专用的媒介，微型驱动程序应执行以下操作的 pin [ *AVStrMiniPinProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556351)函数：

1.  如果驱动程序的自定义为固定连接选择介质 (例如，pin 的介质不是 KSMEDIUMSETID\_标准)，该驱动程序应将通过其专用总线数据的路由。 AVStream 不会启用流指针传输连接使用自定义媒体的 pin。

2.  该驱动程序可以通过调用来确定已连接的针[ **KsPinGetConnectedPinFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff563508)。

3.  然后，驱动程序可以执行对缓冲区的操作，并将其路由到通过其自定义中的已连接的 pin/筛选器对象。

 

 




