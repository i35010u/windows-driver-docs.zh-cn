---
title: 初始化 UMDF 中的常规 I/O 目标
description: 初始化 UMDF 中的常规 I/O 目标
ms.assetid: cf1b39c3-4c82-411b-8eef-117ac0fe793e
keywords:
- 一般 i/o 目标是 WDK UMDF，初始化
- 初始化常规 i/o 目标 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b09f4b7219a814c14533d98132d573097df519a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210599"
---
# <a name="initializing-a-general-io-target-in-umdf"></a>初始化 UMDF 中的常规 I/O 目标


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

驱动程序用来初始化一般 i/o 目标的步骤取决于 i/o 目标是[本地](general-i-o-targets-in-umdf.md)还是远程。

### <a name="initializing-a-local-io-target"></a>初始化本地 i/o 目标

本地 i/o 目标包括设备的[默认 i/o 目标](general-i-o-targets-in-umdf.md)和基于文件句柄的 i/o 目标。

当驱动程序调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法时，框架会为设备初始化驱动程序的默认 i/o 目标。 若要检索允许驱动程序访问设备的默认 i/o 目标的[IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)接口，驱动程序将调用[**IWDFDevice：： GetDefaultIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-getdefaultiotarget)方法。

大多数驱动程序只向其默认 i/o 目标发送请求。

如果 UMDF 驱动程序必须将 i/o 请求发送到基于句柄的接口，例如网络套接字接口，则驱动程序必须创建基于文件句柄的 i/o 目标对象。 若要创建基于文件句柄的 i/o 目标对象，驱动程序必须执行以下操作：

1.  调用设备的[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)接口的**QueryInterface**方法，检索指向[IWDFFileHandleTargetFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffilehandletargetfactory)接口的指针。

2.  通过调用 Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **CreateNamedPipe**或**socket**函数获取文件、命名管道或套接字的 win32 句柄。

3.  调用[**IWDFFileHandleTargetFactory：： CreateFileHandleTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffilehandletargetfactory-createfilehandletarget)方法为文件、管道或套接字创建基于文件句柄的 i/o 目标对象。

有关演示如何检索[IWDFFileHandleTargetFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffilehandletargetfactory)接口，获取 Win32 句柄并创建基于文件句柄的 i/o 目标对象的代码示例，请参阅[**IWDFFileHandleTargetFactory：： CreateFileHandleTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffilehandletargetfactory-createfilehandletarget)中的代码示例。

驱动程序创建基于文件句柄的 i/o 目标后，该驱动程序可以向 i/o 目标发送 i/o 请求。

### <a name="initializing-a-remote-io-target"></a>初始化远程 i/o 目标

在您的驱动程序可以使用远程 i/o 目标之前，它必须创建远程目标对象并打开目标，如下所示：

1.  调用[**IWDFDevice2：： CreateRemoteTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-createremotetarget)以创建远程目标对象。

2.  调用[**IWDFRemoteTarget：： OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname) （对于文件）或[**IWDFRemoteTarget：： OpenRemoteInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface) （对于[设备接口](using-device-interfaces-in-umdf-drivers.md)）以打开 i/o 操作的目标。

 

 





