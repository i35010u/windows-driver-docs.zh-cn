---
title: /Initialize 开关
description: /Initialize 开关将 (ASC) 1667 中存储的身份验证接收器证书初始化为其原始制造商的状态。
keywords:
- /Initialize 交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Initialize
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90a49cf30e8fc666620f67aa9a99de40287a1120
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833149"
---
# <a name="initialize-switch"></a>/Initialize 开关


增强的存储证书管理工具的 **/Initialize** 开关将 (ASC) 1667 中存储的身份验证接收器证书初始化为其原始制造商的状态。

**注意**  在本主题中，指定的与 IEEE 1667 兼容的 USB 存储设备称为 *目标设备*。



```
    EhStorCertMgrCmd /Initialize  -Volume:
    VolumeName 
    [-Quiet]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span>**-Volume：**   
目标设备的卷名。 有关此参数的格式的详细信息，请参阅 [增强的存储证书管理工具概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令提示符下键入 **EhStorCertMgrCmd/list** ，然后按 enter。



<span id="_______-Quiet______"></span><span id="_______-quiet______"></span><span id="_______-QUIET______"></span>**-Quiet**   
当 USB 存储设备初始化时，禁止显示详细输出。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

除了 ASC-manufacturer (ASCm) 证书外， **/Initialize** 开关删除 asc 存储区中的所有证书。 与 [**/Clear 开关**](-clear-switch.md)不同， **/INITIALIZE** 开关从 ASC 存储区中删除预配 (PCp) 证书。

如果使用设置证书为目标设备预配 (PCp) ，则该证书的私钥必须位于主机中，以便通过该设备传递管理身份验证。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何初始化目标设备：

```
EhStorCertMgrCmd /Initialize -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}"
```









