---
title: 检索有关受保护的输出的信息
description: 检索有关受保护的输出的信息
ms.assetid: 20e268b8-fea0-48dd-a3cd-3cbb4233ef99
keywords:
- OPM WDK 显示检索受保护输出信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47cd647618525bf90a3e809ad763a91f0f1f4d98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524686"
---
# <a name="retrieving-information-about-a-protected-output"></a>检索有关受保护的输出的信息


显示微型端口驱动程序可以接收请求来检索有关与图形适配器的物理输出连接器关联的受保护输出的信息。 显示微型端口驱动程序[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)函数传递一个指向[ **DXGKMDT\_OPM\_GET\_INFO\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560868)结构*参数*参数，其中包含信息请求。 *DxgkDdiOPMGetInformation*写入到所需的信息[ **DXGKMDT\_OPM\_请求\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560910)结构*RequestedInformation*参数指向。 **GuidInformation**并**abParameters** DXGKMDT 成员\_OPM\_获取\_信息\_参数指定信息请求。 具体取决于信息请求，显示微型端口驱动程序应填充的成员[ **DXGKMDT\_OPM\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560925)， [**DXGKMDT\_OPM\_输出\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff560890)，或者[ **DXGKMDT\_OPM\_实际\_输出\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff560840)具有所需的信息和点结构**abRequestedInformation** DXGKMDT 成员\_OPM\_请求\_向该结构的信息。 该驱动程序指定后**cbRequestedInformationSize** (例如，sizeof (DXGKMDT\_OPM\_标准\_信息)) 和**abRequestedInformation**DXGKMDT 成员\_OPM\_请求\_信息，该驱动程序必须计算一个密钥加密块链接 (CBC)-DXGKMDT 中的数据的模式消息身份验证代码 (OMAC)\_OPM\_请求\_信息，必须设置此 OMAC **omac** DXGKMDT 成员\_OPM\_请求\_信息。 有关计算 OMAC 的详细信息，请参阅[OMAC 1 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。

**请注意**  之前[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)返回时，显示微型端口驱动程序必须验证中指定 OMAC **omac**的成员[ **DXGKMDT\_OPM\_获取\_信息\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560868)正确无误。 此外必须验证该驱动程序中的序列号，指定**ulSequenceNumber** DXGKMDT 成员\_OPM\_获取\_信息\_参数匹配序列该驱动程序当前存储的数字。 然后，该驱动程序必须递增存储的序列号。

 

**请注意**  驱动程序必须返回的 128 位安全加密随机数字**rnRandomNumber** DXGKMDT 成员\_OPM\_标准\_信息， [ **DXGKMDT\_OPM\_输出\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff560890)，或 DXGKMDT\_OPM\_实际\_输出\_格式。 随机数字生成由发送应用程序和中未提供**rnRandomNumber** DXGKMDT 成员\_OPM\_获取\_信息\_参数。

 

驱动程序返回指示请求的以下信息：

-   有关 DXGKMDT\_OPM\_获取\_支持\_保护\_中设置类型**guidInformation**成员和中未定义**abParameters**隶属 DXGKMDT\_OPM\_获取\_信息\_参数结构，该驱动程序指示可用的一种保护机制。 若要指示可保护类型，该驱动程序返回的值的有效按位 OR 组合[ **DXGKMDT\_OPM\_保护\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff560898)中的枚举**ulInformation** DXGKMDT 成员\_OPM\_标准\_信息。 DXGKMDT\_OPM\_PROTECTION\_类型\_HDCP 和 DXGKMDT\_OPM\_保护\_类型\_DPCP 值是否有效。

-   有关 DXGKMDT\_OPM\_获取\_连接器\_中设置类型**guidInformation**和中未定义**abParameters**，指示该驱动程序连接器类型。 若要指示连接器类型，该驱动程序返回的值的有效按位 OR 组合[ **D3DKMDT\_视频\_输出\_技术**](https://msdn.microsoft.com/library/windows/hardware/ff546605)中的枚举**ulInformation** DXGKMDT 成员\_OPM\_标准\_信息。

-   有关 DXGKMDT\_OPM\_获取\_虚拟\_保护\_级别或 DXGKMDT\_OPM\_获取\_实际\_保护\_级别中设置**guidInformation**中设置保护类型**abParameters**，驱动程序将返回中的保护级别值**ulInformation**成员[ **DXGKMDT\_OPM\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560925)。 保护类型是否为 DXGKMDT\_OPM\_PROTECTION\_类型\_HDCP，保护级别值是从[ **DXGKMDT\_OPM\_HDCP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560878)枚举。 保护类型是否为 DXGKMDT\_OPM\_PROTECTION\_类型\_DPCP，保护级别值是从[ **DXGKMDT\_OPM\_DPCP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560861)枚举。

    DXGKMDT\_OPM\_获取\_虚拟\_保护\_级别请求将返回当前设置为受保护的输出保护级别。 DXGKMDT\_OPM\_获取\_实际\_保护\_级别请求将返回当前设置是与受保护的输出相关的物理连接器的保护级别。

-   有关 DXGKMDT\_OPM\_获取\_适配器\_总线\_中设置类型**guidInformation**和中未定义**abParameters**，驱动程序标识的类型和连接到的母板芯片组北部桥的图形适配器总线实现。 若要标识的类型和总线实现，该驱动程序返回的中值的有效按位 OR 组合[ **DXGKMDT\_OPM\_总线\_类型\_AND\_实现**](https://msdn.microsoft.com/library/windows/hardware/ff560841)中的枚举**ulInformation** DXGKMDT 成员\_OPM\_标准\_信息。

-   有关 DXGKMDT\_OPM\_获取\_当前\_HDCP\_SRM\_版本中设置**guidInformation**和中未定义**abParameters**，该驱动程序返回值以**ulInformation**的成员[ **DXGKMDT\_OPM\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560925)标识的版本号的当前高带宽数字内容保护 (HDCP) 系统可更新性消息 (SRM) 为受保护的输出。 最低有效位 （位 0 到 15） 包含在 little-endian 格式 SRM 的版本号。 有关 SRM 版本号的详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

-   有关 DXGKMDT\_OPM\_获取\_实际\_输出\_格式设置**guidInformation**和中未定义**abParameters**、驱动程序中的成员返回的信息[ **DXGKMDT\_OPM\_实际\_输出\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff560840) ，用于描述如何格式化受保护的输出与相关联的物理连接器将经历的信号。

-   有关 DXGKMDT\_OPM\_获取\_输出\_ID 在中设置**guidInformation**和中未定义**abParameters**，驱动程序将返回中的信息成员[ **DXGKMDT\_OPM\_输出\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff560890) ，用于标识输出连接器。

-   有关 DXGKMDT\_OPM\_获取\_DVI\_中设置特征**guidInformation**成员和中未定义**abParameters**的成员DXGKMDT\_OPM\_获取\_信息\_参数结构，该驱动程序指示电气特征的数字视频接口 (DVI) 输出连接器。 若要指示 DVI 电气特征，驱动程序返回的值之一[ **DXGKDT\_OPM\_DVI\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff560819)中的枚举**ulInformation**的成员[ **DXGKMDT\_OPM\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560925)。

 

 





