---
title: 64 位系统上的设备安装
description: 64 位系统上的设备安装
ms.assetid: 76d9bff7-6429-4d20-9790-a41ed2cb1bdd
keywords:
- 64 位 WDK 设备安装
- 设备安装 WDK，64 位系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b3ee167eb7c8f690175b440f4a45e48c0112d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387128"
---
# <a name="device-installations-on-64-bit-systems"></a>64 位系统上的设备安装





如果你的设备将安装在 32 位平台和 64 位平台上，在创建时，必须执行以下步骤[驱动程序包](driver-packages.md):

-   提供的所有内核模式驱动程序的 32 位和 64 位编译*设备安装应用程序*，*类安装程序*，并*共同安装程序*。 有关详细信息，请参阅[移植您驱动程序添加到 64 位 Windows](https://docs.microsoft.com/windows-hardware/drivers/kernel/porting-your-driver-to-64-bit-windows)。

-   提供一个或多个使用的跨平台 INF 文件*修饰 INF 部分*以控制特定于平台的安装行为。

你是否[编写设备安装应用程序](writing-a-device-installation-application.md)，32 位版本必须是默认版本。 也就是说，32 位版本应自动运行 （Microsoft Windows SDK 文档中所述），通过调用，以便用户插入您分发的磁盘时自动启动。

32 位版本的应用程序必须检查返回的值[ **UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)。 如果返回值为 ERROR_IN_WOW64，32 位应用程序在 64 位平台上执行，并不能更新收件箱驱动程序。 相反，它必须调用[ **CreateProcess** ](https://docs.microsoft.com/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessa) （Windows SDK 文档中所述） 来启动应用程序的 64 位版本。 然后可以调用的是 64 位版本**UpdateDriverForPlugAndPlayDevices**，并指定*FullInfPath*参数标识的 64 位版本的所有文件的位置。

 

 





