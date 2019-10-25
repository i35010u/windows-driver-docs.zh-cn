---
title: 在 AVStream 编解码器中使用硬件媒体
description: 在 AVStream 编解码器中使用硬件媒体
ms.assetid: 07c25875-c549-4d47-ac0d-605f2aa9daa4
keywords:
- AVStream 硬件编解码器支持 WDK，使用硬件介质
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcdfa1dab865d860c142a08fce7435519d1aa75e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842295"
---
# <a name="using-hardware-mediums-in-avstream-codecs"></a>在 AVStream 编解码器中使用硬件媒体


支持专用媒体的 AVStream 微型驱动程序可以传输设备硬件中的数据，而无需对系统内存进行中间传输。

具体来说，如果两个筛选器共享同一专用中型和中型实例，媒体基础仅在设备硬件中传输介质。 此传输发生，而不将函数引入系统内存。 例如，来自同一设备的解码器和编码器可以共享专用介质，这会显著提高性能。

若要使用专用媒体，微型驱动程序应在 pin 的[*AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)函数中执行以下操作：

1.  如果为 pin 连接选择了驱动程序的自定义介质（例如，pin 的媒体不 KSMEDIUMSETID\_Standard），则驱动程序应通过其专用总线来路由数据。 AVStream 不会为使用自定义媒体连接的 pin 启用流指针传输。

2.  驱动程序可以通过调用[**KsPinGetConnectedPinFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetconnectedpinfileobject)来确定连接的 pin。

3.  然后，该驱动程序可以对该缓冲区执行操作，并通过其自定义媒体将其路由到连接的 pin/筛选器对象。

 

 




