---
title: /Clear 开关
description: 增强的存储证书管理工具的/Clear 开关将从身份验证接收器证书中删除大多数证书， (ASC) 存储在指定的符合 IEEE 1667 的 USB 存储设备上。请注意，在本主题中，指定的与 IEEE 1667 兼容的 USB 存储设备称为目标设备。
keywords:
- /Clear 交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Clear
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eb4f477d386f8ceecd863bed0f9f606eb97b271
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833583"
---
# <a name="clear-switch"></a>/Clear 开关


增强的存储证书管理工具的 **/Clear** 开关将从身份验证接收器证书中删除大多数证书， (ASC) 存储在指定的符合 IEEE 1667 的 USB 存储设备上。

**注意**  在本主题中，指定的与 IEEE 1667 兼容的 USB 存储设备称为 *目标设备*。



```
    EhStorCertMgrCmd /Clear  -Volume:
    VolumeName
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume______"></span><span id="_______-volume______"></span><span id="_______-VOLUME______"></span>**-卷**   
目标设备的卷名。 有关此参数的格式的详细信息，请参阅 [增强的存储证书管理工具概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令提示符下键入 **EhStorCertMgrCmd/list** ，然后按 enter。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/Clear** 开关从目标设备中清除除以下证书之外的所有证书：

-   设置证书 (PCp) 。 若要删除 PCp 证书，必须使用 [**/Initialize 开关**](-initialize-switch.md)。

-   ASC-制造商证书 (ASCm) 。

    **注意**   增强的存储证书管理工具无法在目标设备中添加、删除或替换 asc 制造商 (ASCm) 证书。



若要清除目标设备中的证书，必须使用 PCp 证书对设备进行预配，并且该证书的私钥必须位于主机中才能通过设备进行管理身份验证。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何从目标设备中清除证书：

```
EhStorCertMgrCmd /Clear -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}"
```





