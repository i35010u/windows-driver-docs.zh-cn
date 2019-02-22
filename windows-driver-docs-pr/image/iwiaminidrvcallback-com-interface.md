---
title: IWiaMiniDrvCallBack COM Interface
description: IWiaMiniDrvCallBack COM Interface
ms.assetid: a535d718-e34f-4cd0-9137-83d28d0b8e9c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30ac6cf3725190c975b8fbe2db49f26b08b6dacb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547544"
---
# <a name="iwiaminidrvcallback-com-interface"></a>IWiaMiniDrvCallBack COM Interface





[IWiaMiniDrvCallBack 接口](https://msdn.microsoft.com/library/windows/hardware/ff543943)提供微型驱动程序和应用程序之间的通信链中的一个链接。 因为微型驱动程序无法直接与应用程序进行通信，反之亦然，二者之间的任何通信必须经过一个中介： WIA 服务。 若要启用此通信，该应用程序实现**IWiaDataCallback**接口 （Microsoft Windows SDK 文档中所述）。 此接口包含**IWiaDataCallback::BandedDataCallback** WIA 服务可以调用的方法。 如果应用程序提供了此回调例程，WIA 服务会创建另一个回调[ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)方法，它提供以供微型驱动程序。

当微型驱动程序已准备就绪，若要从映像创建的设备发送图像数据或将状态消息 （例如传输的数据的百分比） 时，它将调用 WIA 服务**IWiaMiniDrvCallBack**::**MiniDrvCallback**。 WIA 服务然后将传递的数据或沿消息给应用程序时它将调用应用程序的回调。

 

 




