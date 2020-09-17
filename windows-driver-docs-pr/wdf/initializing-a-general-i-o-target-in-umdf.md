---
title: 初始化 UMDF 中的常规 I/O 目标
description: 初始化 UMDF 中的常规 I/O 目标
ms.assetid: cf1b39c3-4c82-411b-8eef-117ac0fe793e
keywords:
- 一般 i/o 目标是 WDK UMDF，初始化
- 初始化常规 i/o 目标 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76acdbcdd0ea6f7d8c0a132c4cfce89a4020d8cf
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716652"
---
# <a name="initializing-a-general-io-target-in-umdf"></a>初始化 UMDF 中的常规 I/O 目标


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

驱动程序用来初始化一般 i/o 目标的步骤取决于 i/o 目标是 [本地](general-i-o-targets-in-umdf.md) 还是远程。

### <a name="initializing-a-local-io-target"></a>初始化本地 i/o 目标

本地 i/o 目标包括设备的 [默认 i/o 目标](general-i-o-targets-in-umdf.md) 和基于文件句柄的 i/o 目标。

当驱动程序调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice) 方法时，框架会为设备初始化驱动程序的默认 i/o 目标。 若要检索允许驱动程序访问设备的默认 i/o 目标的 [IWDFIoTarget](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget) 接口，驱动程序将调用 [**IWDFDevice：： GetDefaultIoTarget**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-getdefaultiotarget) 方法。

大多数驱动程序只向其默认 i/o 目标发送请求。

如果 UMDF 驱动程序必须将 i/o 请求发送到基于句柄的接口，例如网络套接字接口，则驱动程序必须创建基于文件句柄的 i/o 目标对象。 若要创建基于文件句柄的 i/o 目标对象，驱动程序必须执行以下操作：

1.  调用设备的[IWDFDevice](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)接口的**QueryInterface**方法，检索指向[IWDFFileHandleTargetFactory](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffilehandletargetfactory)接口的指针。

2.  通过调用 Win32 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **CreateNamedPipe**或 **socket** 函数获取文件、命名管道或套接字的 win32 句柄。

3.  调用 [**IWDFFileHandleTargetFactory：： CreateFileHandleTarget**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffilehandletargetfactory-createfilehandletarget) 方法为文件、管道或套接字创建基于文件句柄的 i/o 目标对象。

有关演示如何检索 [IWDFFileHandleTargetFactory](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffilehandletargetfactory) 接口，获取 Win32 句柄并创建基于文件句柄的 i/o 目标对象的代码示例，请参阅 [**IWDFFileHandleTargetFactory：： CreateFileHandleTarget**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffilehandletargetfactory-createfilehandletarget)中的代码示例。

驱动程序创建基于文件句柄的 i/o 目标后，该驱动程序可以向 i/o 目标发送 i/o 请求。

### <a name="initializing-a-remote-io-target"></a>初始化远程 i/o 目标

在您的驱动程序可以使用远程 i/o 目标之前，它必须创建远程目标对象并打开目标，如下所示：

1.  调用 [**IWDFDevice2：： CreateRemoteTarget**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-createremotetarget) 以创建远程目标对象。

2.  为 "[设备) 接口](using-device-interfaces-in-umdf-drivers.md)") 或[**IWDFRemoteTarget：： OpenRemoteInterface**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface) (调用[**IWDFRemoteTarget：： OpenFileByName**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname) (，以打开 i/o 操作的目标。

 

