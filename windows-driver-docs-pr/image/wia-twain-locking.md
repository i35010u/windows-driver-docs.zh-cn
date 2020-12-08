---
title: WIA-TWAIN 锁定
description: WIA-TWAIN 锁定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbc6d41515330b56720833780d5b82a41c5d06cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826377"
---
# <a name="wia-twain-locking"></a>WIA-TWAIN 锁定





对于使用不同锁定机制的 TWAIN 驱动程序和 WIA 驱动程序，当 WIA 驱动程序访问设备时，TWAIN 驱动程序应无法同时访问设备。 这可能会导致此类问题，如映像损坏和传输失败。

TWAIN 硬件通常随附供应商提供的实用程序或应用程序软件来执行诊断、传输数据和发送传真。 此供应商提供的软件可能会直接访问 STI 驱动程序，而不是通过 WIA 服务访问。 不建议这样做，这可能会导致锁定问题。 例如，如果供应商提供的应用程序软件访问设备并直接锁定设备，则在应用程序解除锁定之前，WIA 应用程序将无法使用该设备。 如果应用程序是一种工具，该工具监视设备并显示在通知区域中 (之前称为系统托盘) ，则不允许在其他特定于供应商的应用程序私下请求它之前释放该锁。

因此，在使用此供应商提供的软件时，请确保遵守可靠的锁定和解锁技术。 这可确保当 WIA 服务轮询设备或传输数据时，它不会中断其他传输 (例如，通过 TWAIN) ，并且 WIA 服务本身不会中断。 请确保只有一个系统获取指定的事件。 也就是说，如果在扫描仪上推送该按钮，WIA 服务将不会在供应商提供的软件启动自己的应用程序的同时启动已注册的 WIA 应用程序。

有关其他信息，请参阅 [锁定和解锁最佳实践](locking-and-unlocking-best-practices.md)。

 

 




