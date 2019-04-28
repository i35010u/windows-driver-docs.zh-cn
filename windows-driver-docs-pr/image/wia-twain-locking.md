---
title: WIA-TWAIN 锁定
description: WIA-TWAIN 锁定
ms.assetid: bf2dc7f5-f3a0-4c51-86e1-854d0704074a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc6180e98766c7c3ee83fad88a1423a7c63c2b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344328"
---
# <a name="wia-twain-locking"></a>WIA-TWAIN 锁定





TWAIN 驱动程序和 WIA 驱动程序的使用不同的锁定机制，当 WIA 驱动程序访问设备，TWAIN 驱动程序时应不能同时访问设备。 这可能会导致损坏映像所遇到的问题和失败传输。

TWAIN 硬件通常会出现与供应商提供的实用程序或应用程序软件，以执行诊断，传输的数据，并发送传真。 此供应商提供的软件可能会通过 WIA 服务访问的 STI 驱动程序直接而不是。 这不建议，并可以引入的锁定问题。 例如，如果供应商提供的应用程序软件访问该设备，并直接将其锁定，然后没有 WIA 应用程序将能够使用该设备，直到应用程序释放该锁。 如果应用程序是一个工具，用于监视设备，并显示在通知区域 （以前称为系统任务栏） 中，它不是允许释放锁，直到另一个特定于供应商的应用程序隐含要求到它。

因此，当您使用此供应商提供的软件，请确保遵守可靠锁定和解锁的技术。 这可确保，当 WIA 服务轮询设备或将数据传输时，它不会中断 （例如，通过 TWAIN)，另一个传输和 WIA 服务是本身同样不中断。 请确保只有一个系统获取指定的事件。 也就是说，如果您在扫描仪上按下按钮，WIA 服务不会启动供应商提供软件启动其自己的应用程序的同时已注册的 WIA 应用程序。

有关其他信息，请参阅[锁定和解锁的最佳实践](locking-and-unlocking-best-practices.md)。

 

 




