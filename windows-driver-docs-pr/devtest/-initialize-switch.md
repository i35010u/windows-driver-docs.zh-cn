---
title: /Initialize 开关
description: /Initialize 交换机初始化身份验证接收器证书 (ASC) 存储 IEEE 1667 合规 USB 存储设备中，为其原始制造商的状态。
ms.assetid: 4e04a099-8ad6-4eb6-9ac7-d466b7d828d4
keywords:
- / 初始化交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Initialize
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b49f3b681ac55767f6908c299afb2b95e4ef9f3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361498"
---
# <a name="initialize-switch"></a>/Initialize 开关


**/初始化**增强存储证书管理工具的开关初始化身份验证接收器证书 (ASC) 存储 IEEE 1667 合规 USB 存储设备中，为其原始制造商的状态。

**请注意**在本主题中，指定的 IEEE 1667 合规 USB 存储设备称为*目标设备*。



```
    EhStorCertMgrCmd /Initialize  -Volume:
    VolumeName 
    [-Quiet]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-卷：**   
目标设备的卷名称。 此参数的格式的详细信息，请参阅[增强存储证书管理工具的概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**请注意**若要生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表，请键入**EhStorCertMgrCmd /List**在命令提示符，然后按 Enter。



<span id="_______-Quiet______"></span><span id="_______-quiet______"></span><span id="_______-QUIET______"></span> **-Quiet**   
初始化 USB 存储设备时，会抑制 verbose 输出。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/初始化**开关从 ASC 制造商 (ASCm) 证书除外 ASC 存储区中移除所有证书。 与不同[ **/Clear 开关**](-clear-switch.md)，则 **/初始化**开关从 ASC 存储中删除预配 (PCp) 证书。

如果目标设备的设置时使用的预配证书 (PCp)，该证书的私钥必须驻留在主机以与设备一起传递管理身份验证。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何初始化的目标设备：

```
EhStorCertMgrCmd /Initialize -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}"
```









