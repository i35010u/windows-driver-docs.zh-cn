---
title: 用于串行服务的注册表设置
description: 用于串行服务的注册表设置
ms.assetid: 5c4a28ab-e2e5-45b4-8179-6f5d40e9c98c
keywords:
- 串行服务 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf34c958de7cdd09e6fabfbb5b913fbfb472381a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388043"
---
# <a name="registry-settings-for-the-serial-service"></a>用于串行服务的注册表设置





本主题介绍序列应用对所有串行设备的哪些序列是功能驱动程序或较低级别设备筛选器驱动程序的注册表设置。

加载后，序列将查询服务条目的值。 如果条目值不存在，序列将添加服务条目值。 序列将项值设置为系统提供 Serial.sys 驱动程序中以静态方式定义的默认值。 如果加载序列之后，更改服务条目值下, 一步时加载序列将使用新值。

序列使用以下服务条目值下的 **...\\Services\\串行**注册表项：

<a href="" id="forcefifoenable--reg-dword-"></a>**ForceFifoEnable** (REG\_DWORD)  
指定一个布尔标志，指示是否强制使用 FIFOs 的序列。 如果**ForceFifofEnable**为非零值，FIFOs 习惯，而不考虑是否序列可以检测 FIFOs 的状态。 否则，仅当序列可以检测它们使用 FIFOs。 默认值为非零值。 如果将项值不存在，设置序列**ForceFifoEnable**条目值，为默认值。 检测的方法的详细信息，请参阅[串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub 上。

<a href="" id="rxfifo--reg-dword-"></a>**RxFIFO** (REG\_DWORD)  
在接收触发端口中断的先进先出指定字节的数。 有关有效的值，请参阅 Serial.h 标头文件中定义的常量[串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub 上。 默认值**RxFIFO**为 8 个字节。 如果将项值不存在，设置序列**RxFIFO**条目值，为默认值。

<a href="" id="txfifo--reg-dword-"></a>**TxFIFO** (REG\_DWORD)  
指定在传输触发端口中断的先进先出的字节数。 有关有效的值，请参阅 Serial.h 标头文件中定义的常量[串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub 上。 默认值**TxFIFO**是 14 个字节。 如果将项值不存在，设置序列**TxFIFO**条目值，为默认值。

<a href="" id="permitshare--reg-dword-"></a>**PermitShare** (REG\_DWORD)  
指定一个布尔标志，指示是否允许系统以共享一个端口使用的中断。 如果**PermitShare**为非零值，中断可以共享; 否则，不能共享中断。 默认值**PermitShare**为 0x00000000。 如果将项值不存在，设置序列**PermitShare**条目值，为默认值。

<a href="" id="breakonentry--debuglevel--and-logfifo"></a>**BreakOnEntry**， **DebugLevel**，和**LogFifo**  
指定用于调试的条目的值。 有关这些项值的详细信息，请参阅 WDK 中包含的串行示例代码。

 

 




