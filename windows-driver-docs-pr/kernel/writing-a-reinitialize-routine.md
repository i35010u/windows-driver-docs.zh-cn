---
title: 编写 Reinitialize 例程
description: 编写 Reinitialize 例程
ms.assetid: 47a7dd3f-e474-49c7-adf2-11f6e788c261
keywords:
- 标准驱动程序例程 WDK 内核，重新初始化例程
- 驱动程序例程 WDK 内核，重新初始化例程
- 例程 WDK 内核，重新初始化例程
- 重新初始化
- 重新初始化驱动程序 WDK
- 驱动程序进行重新初始化 WDK 内核
- 驱动程序初始化 WDK 内核
- 初始化驱动程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 915014aa9747ae48ab802650b7764a1dafd07daf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374157"
---
# <a name="writing-a-reinitialize-routine"></a>编写 Reinitialize 例程





可以包含任何驱动程序，需要在阶段中初始化其自身[*重新初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)例程。 一个*重新初始化*后，会调用例程[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程返回控件和其他驱动程序已初始化自身。 通常情况下，*重新初始化*例程执行另一个驱动程序启动后必须完成的任务。

例如，系统的键盘类驱动程序， **kbdclass**，支持即插即用以及传统键盘的两个端口。 如果一个系统都包含一个或多个 PnP 管理器无法检测到的旧端口，在键盘类驱动程序必须不过创建每个端口和基于端口的较低级驱动程序本身层的设备对象。 因此，在类驱动程序还拥有*重新初始化*例程的调用后其**DriverEntry**并[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程具有已调用和其他驱动程序已加载。 *重新初始化*例程检测到该端口，创建一个设备对象，和层通过其他低级驱动程序设备驱动程序。

驱动程序的[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程调用[ **IoRegisterDriverReinitialization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterdriverreinitialization)到队列*重新初始化*例程的执行。 *重新初始化*还可以调用例程**IoRegisterDriverReinitialization**本身，这会导致例程进行重新排队。 参数之一*重新初始化*指示它已被调用的次数。

在调用**IoRegisterDriverReinitialization**可以包括驱动程序定义的上下文数据，则系统将提供作为输入的指针*重新初始化*。 如果*重新初始化*例程使用注册表，上下文数据应包括*RegistryPath*指针传递给**DriverEntry**例程因为这指针不是输入的参数*重新初始化*例程。

*重新初始化*如果不会调用例程**DriverEntry**不会返回状态\_成功。

通常情况下，驱动程序和*重新初始化*例程是控制即插即用和旧设备的更高级别的驱动程序。 除了创建设备对象的设备的即插即用管理器检测到 (和 PnP 管理器调用的驱动程序*AddDevice*例程)，该驱动程序还必须创建设备对象的旧设备的即插即用管理器不会枚举。 *重新初始化*例程创建了这些设备对象和层驱动程序通过基础设备的下一步低驱动程序。

如果驱动程序包含*重新初始化*中所述的相同基本步骤在初始化例程，[编写 DriverEntry 例程](writing-a-driverentry-routine.md)，并且也包含与相同的基本要求其**DriverEntry**例程。

 

 




