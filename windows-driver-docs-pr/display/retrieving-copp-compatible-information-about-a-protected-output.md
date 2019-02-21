---
title: 检索受保护的输出 COPP 兼容信息
description: 显示微型端口驱动程序可以接收请求来检索有关与图形适配器的物理输出连接器关联的受保护输出 COPP 兼容信息。
ms.assetid: 9114f232-4123-47a8-b43d-62d14b9f6b08
keywords:
- OPM WDK 显示，检索 COPP 兼容信息
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 3d8a6c83ae7aa46153de12437537a871fee99661
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522240"
---
# <a name="retrieving-copp-compatible-information-on-protected-output"></a>检索受保护的输出 COPP 兼容信息


显示微型端口驱动程序可以接收请求来检索有关与图形适配器的物理输出连接器关联的受保护输出 COPP 兼容信息。 显示微型端口驱动程序[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)函数传递一个指向[ **DXGKMDT\_OPM\_COPP\_兼容\_获取\_信息\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560859)结构*参数*参数，其中包含信息请求。 *DxgkDdiOPMGetCOPPCompatibleInformation*写入到所需的信息[ **DXGKMDT\_OPM\_请求\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560910)结构的*RequestedInformation*参数指向。 **GuidInformation**并**abParameters** DXGKMDT 成员\_OPM\_COPP\_兼容\_获取\_信息\_参数指定信息请求。 具体取决于信息请求，显示微型端口驱动程序应填充的成员[ **DXGKMDT\_OPM\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560925)， [**DXGKMDT\_OPM\_实际\_输出\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff560840)， [ **DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_信号发送**](https://msdn.microsoft.com/library/windows/hardware/ff560830)，或者[ **DXGKMDT\_OPM\_已连接\_HDCP\_设备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560854)具有所需的信息和点结构**abRequestedInformation** DXGKMDT 成员\_OPM\_请求\_向该结构的信息。 该驱动程序指定后**cbRequestedInformationSize** (例如， <strong>sizeof (</strong>DXGKMDT\_OPM\_标准\_信息<strong>)</strong>) 和**abRequestedInformation** DXGKMDT 成员\_OPM\_请求\_信息，该驱动程序必须计算一个密钥加密块链接 (CBC)-DXGKMDT 中的数据的模式消息身份验证代码 (OMAC)\_OPM\_请求\_信息，必须设置此 OMAC **omac** DXGKMDT 成员\_OPM\_请求\_信息。 有关计算 OMAC 的详细信息，请参阅[OMAC 1 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。

**请注意**  之前[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)返回时，必须验证是否显示微型端口驱动程序的序列号，中指定**ulSequenceNumber** DXGKMDT 成员\_OPM\_COPP\_兼容\_获取\_信息\_参数匹配的序列号，该驱动程序当前已存储。 然后，该驱动程序必须递增存储的序列号。

 

**请注意**  驱动程序必须返回的 128 位安全加密随机数字**rnRandomNumber** DXGKMDT 成员\_OPM\_标准\_信息、 DXGKMDT\_OPM\_实际\_输出\_格式、 DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_发出信号，或 DXGKMDT\_OPM\_CONNECTED\_HDCP\_设备\_信息。 随机数字生成由发送应用程序和中未提供**rnRandomNumber** DXGKMDT 成员\_OPM\_COPP\_兼容\_获取\_信息\_参数。

 

驱动程序返回指示请求的以下信息：

-   有关 DXGKMDT\_OPM\_获取\_支持\_保护\_中设置类型**guidInformation**成员和中未定义**abParameters**隶属 DXGKMDT\_OPM\_COPP\_兼容\_获取\_信息\_参数，该驱动程序指示可用的一种保护机制。 若要指示可保护类型，该驱动程序返回的值的有效按位 OR 组合[ **DXGKMDT\_OPM\_保护\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff560898)中的枚举**ulInformation** DXGKMDT 成员\_OPM\_标准\_信息。 DXGKMDT\_OPM\_PROTECTION\_类型\_ACP、 DXGKMDT\_OPM\_保护\_类型\_CGMSA 和 DXGKMDT\_OPM\_保护\_类型\_COPP\_兼容\_HDCP 值是否有效。

-   有关 DXGKMDT\_OPM\_获取\_连接器\_中设置类型**guidInformation**和中未定义**abParameters**，指示该驱动程序连接器类型。 若要指示连接器类型，该驱动程序返回的值的有效按位 OR 组合[ **D3DKMDT\_视频\_输出\_技术**](https://msdn.microsoft.com/library/windows/hardware/ff546605)中的枚举**ulInformation** DXGKMDT 成员\_OPM\_标准\_信息。

-   有关 DXGKMDT\_OPM\_获取\_虚拟\_保护\_级别或 DXGKMDT\_OPM\_获取\_实际\_保护\_级别中设置**guidInformation**中设置保护类型**abParameters**，驱动程序将返回中的保护级别值**ulInformation**成员[ **DXGKMDT\_OPM\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560925)。 保护类型是否为 DXGKMDT\_OPM\_PROTECTION\_类型\_ACP，保护级别值是从[ **DXGKMDT\_OPM\_ACP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560834)枚举。 保护类型是否为 DXGKMDT\_OPM\_PROTECTION\_类型\_CGMSA，保护级别值是从[ **DXGKMDT\_OPM\_CGMSA**](https://msdn.microsoft.com/library/windows/hardware/ff560846)枚举。 保护类型是否为 DXGKMDT\_OPM\_PROTECTION\_类型\_COPP\_兼容\_HDCP，保护级别值是从[ **DXGKMDT\_OPM\_HDCP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560878)枚举。

    DXGKMDT\_OPM\_获取\_虚拟\_保护\_级别请求将返回当前设置为受保护的输出保护级别。 DXGKMDT\_OPM\_获取\_实际\_保护\_级别请求将返回当前设置是与受保护的输出相关的物理连接器的保护级别。

-   有关 DXGKMDT\_OPM\_获取\_适配器\_总线\_中设置类型**guidInformation**和中未定义**abParameters**，驱动程序标识将图形适配器连接到的母板芯片组北部桥的总线类型。 若要标识的总线类型，驱动程序返回的值的有效按位 OR 组合[ **DXGKMDT\_OPM\_总线\_类型\_AND\_实现** ](https://msdn.microsoft.com/library/windows/hardware/ff560841)中的枚举**ulInformation** DXGKMDT 成员\_OPM\_标准\_信息。

    该驱动程序只能合并 DXGKMDT\_OPM\_COPP\_兼容\_总线\_类型\_集成 (0x80000000) 值的其中一个总线类型值时无接口使用公开提供的规范和标准连接器类型的扩展总线上提供了图形适配器和其他子系统之间的信号。 内存总线不在此定义。

-   有关 DXGKMDT\_OPM\_获取\_实际\_输出\_格式设置**guidInformation**和中未定义**abParameters**、驱动程序中的成员返回的信息[ **DXGKMDT\_OPM\_实际\_输出\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff560840) ，用于描述如何格式化受保护的输出与相关联的物理连接器将经历的信号。

-   有关 DXGKMDT\_OPM\_获取\_ACP\_AND\_CGMSA\_中设置的信号发送**guidInformation**和中未定义**abParameters**，该驱动程序中的成员返回的信息[ **DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_信号发送**](https://msdn.microsoft.com/library/windows/hardware/ff560830) ，用于描述如何保护受保护的输出与相关联的物理连接器将经历的信号。

-   有关 DXGKMDT\_OPM\_获取\_已连接\_HDCP\_设备\_中的信息集合**guidInformation**和中未定义**abParameters**，该驱动程序中的成员返回的信息[ **DXGKMDT\_OPM\_已连接\_HDCP\_设备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560854)包含高带宽数字内容保护 (HDCP) 信息。

 

 





