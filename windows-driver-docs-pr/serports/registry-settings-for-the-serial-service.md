---
title: 用于串行服务的注册表设置
description: 用于串行服务的注册表设置
ms.assetid: 5c4a28ab-e2e5-45b4-8179-6f5d40e9c98c
keywords:
- 串行服务 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7215bc17f2a69f60ac595ddec462b77a90040f6c
ms.sourcegitcommit: 6b09412f7bf562f7c01ffa94ac44a3d0ea895e3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82086711"
---
# <a name="registry-settings-for-the-serial-service"></a>用于串行服务的注册表设置





本主题介绍串行适用于所有串行设备的注册表设置，串行设备是其功能驱动程序或较低级别的设备筛选器驱动程序。

序列会在加载服务输入值后对其进行查询。 如果条目值不存在，则序列将添加服务条目值。 串行将输入值设置为系统提供的 sys.databases 驱动程序中静态定义的默认值。 如果在加载串行后更改服务条目值，则会在下一次加载串行时使用新值。

串行使用下的以下服务条目值 **。服务\\序列注册表\\**项：

<a href="" id="forcefifoenable--reg-dword-"></a>**ForceFifoEnable** （REG\_DWORD）  
指定一个布尔型标志，该标志指示是否强制串行使用 FIFOs。 如果**ForceFifofEnable**为非零，则将使用 FIFOs，而不管串行能否检测是否存在 FIFOs。 否则，FIFOs 仅在串行可以检测到它们时使用。 的默认值为非零值。 如果条目值不存在，则 Serial 会将**ForceFifoEnable**输入值设置为默认值。 有关检测方法的详细信息，请参阅 GitHub 上的[串行驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)。

<a href="" id="rxfifo--reg-dword-"></a>**RxFIFO** （REG\_DWORD）  
指定接收 FIFO 中触发端口中断的字节数。 有关有效值，请参阅 GitHub 上的[串行驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)中的 serial 标头文件中定义的常量。 **RxFIFO**的默认值为8个字节。 如果条目值不存在，则 Serial 会将**RxFIFO**输入值设置为默认值。

<a href="" id="txfifo--reg-dword-"></a>**TxFIFO** （REG\_DWORD）  
指定传输 FIFO 中触发端口中断的字节数。 有关有效值，请参阅 GitHub 上的[串行驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)中的 serial 标头文件中定义的常量。 **TxFIFO**的默认值为14个字节。 如果条目值不存在，则 Serial 会将**TxFIFO**输入值设置为默认值。

<a href="" id="permitshare--reg-dword-"></a>**PermitShare** （REG\_DWORD）  
指定一个布尔型标志，该标志指示是否允许系统共享端口使用的中断。 如果**PermitShare**为非零，则可以共享中断;否则，中断无法共享。 **PermitShare**的默认值为0x00000000。 如果条目值不存在，则 Serial 会将**PermitShare**输入值设置为默认值。

<a href="" id="breakonentry--debuglevel--and-logfifo"></a>**BreakOnEntry**、 **DebugLevel**和**LogFifo**  
指定用于调试的条目值。 有关这些输入值的详细信息，请参阅 WDK 中包含的串行示例代码。

 

 




