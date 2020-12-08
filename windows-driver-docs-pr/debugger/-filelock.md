---
title: filelock
description: Filelock 扩展显示文件锁结构。
keywords:
- filelock Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- filelock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2bc0136e6704da4ffc946101c2e7d307d31cbb84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821697"
---
# <a name="filelock"></a>!filelock


**！ Filelock** extension 显示文件锁结构。

语法

```dbgcmd
!filelock FileLockAddress 
!filelock ObjectAddress 
```

## <a name="span-idddk__filelock_dbgspanspan-idddk__filelock_dbgspanparameters"></a><span id="ddk__filelock_dbg"></span><span id="DDK__FILELOCK_DBG"></span>参数


<span id="_______FileLockAddress______"></span><span id="_______filelockaddress______"></span><span id="_______FILELOCKADDRESS______"></span>*FileLockAddress*   
指定文件锁结构的十六进制地址。

<span id="_______ObjectAddress______"></span><span id="_______objectaddress______"></span><span id="_______OBJECTADDRESS______"></span>*ObjectAddress*   
指定拥有文件锁的文件对象的十六进制地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关文件对象的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

 

 





