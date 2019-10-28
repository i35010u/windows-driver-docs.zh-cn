---
title: 编写 Reinitialize 例程
description: 编写 Reinitialize 例程
ms.assetid: 47a7dd3f-e474-49c7-adf2-11f6e788c261
keywords:
- 标准驱动程序例程 WDK 内核，重新初始化例程
- 驱动程序例程 WDK 内核，重新初始化例程
- 例程 WDK 内核，重新初始化例程
- 初始化
- 重新初始化驱动程序 WDK
- 驱动程序重新初始化 WDK 内核
- 驱动程序初始化 WDK 内核
- 初始化驱动程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d038c38963eba02e6d78412bf928b182a3ad19d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835605"
---
# <a name="writing-a-reinitialize-routine"></a>编写 Reinitialize 例程





需要在各个阶段初始化自身的任何驱动程序都可以包含一个重新[*初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)例程。 重新*初始化*例程将在[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程返回控件和其他驱动程序自行初始化之后调用。 通常，重新*初始化*例程执行必须在另一个驱动程序启动之后完成的任务。

例如，系统的键盘类驱动程序**kbdclass**支持 PnP 和旧键盘端口。 如果系统包含一个或多个 PnP 管理器无法检测到的旧版端口，则键盘类驱动程序必须为每个端口创建一个设备对象，并在端口的较低级别驱动程序上创建层级。 因此，在调用**DriverEntry**和[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程并加载其他驱动程序之后，该类驱动程序具有要调用的*初始化*例程。 重新*初始化*例程将检测端口，为其创建一个设备对象，并将该驱动程序与该设备的其他较低级驱动程序进行分层。

驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用[**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)将重新*初始化*例程排队等待执行。 重新*初始化*例程还可以调用**IoRegisterDriverReinitialization**本身，这将导致例程被重新排队。 要重新*初始化*的参数之一指示它被调用的次数。

对**IoRegisterDriverReinitialization**的调用可以包含指向驱动程序定义的上下文数据的指针，系统会将该指针作为输入提供给进行重新*初始化*。 如果重新*初始化*例程使用注册表，则上下文数据应包括传递到**DriverEntry**例程的*RegistryPath*指针，因为此指针不是重新*初始化*例程的输入参数。

如果**DriverEntry**不返回状态\_成功，则不会调用重新*初始化*例程。

通常，具有重新*初始化*例程的驱动程序是控制 PnP 和旧设备的更高级别的驱动程序。 除了为 pnp 管理器检测到的设备（PnP 管理器调用驱动程序的*AddDevice*例程）创建设备对象外，驱动程序还必须为 pnp 管理器不枚举的旧设备创建设备对象。 重新*初始化*例程将创建这些设备对象，并通过基础设备的下一个较低驱动程序对驱动程序进行分层。

如果驱动程序具有重新*初始化*例程，它将在[编写 DriverEntry 例程](writing-a-driverentry-routine.md)时所述的相同基本步骤中进行初始化，并且它还具有与**DriverEntry**例程相同的基本要求。

 

 




