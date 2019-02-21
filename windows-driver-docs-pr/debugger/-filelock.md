---
title: filelock
description: Filelock 扩展显示文件锁结构。
ms.assetid: 943a0ed8-b7a5-4ab6-8579-6a27e06e1dac
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
ms.openlocfilehash: d17027482c4a1ca471c7b8abeab57d8999bd6b5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519888"
---
# <a name="filelock"></a>！ filelock


**！ Filelock**扩展显示文件锁结构。

语法

```dbgcmd
!filelock FileLockAddress 
!filelock ObjectAddress 
```

## <a name="span-idddkfilelockdbgspanspan-idddkfilelockdbgspanparameters"></a><span id="ddk__filelock_dbg"></span><span id="DDK__FILELOCK_DBG"></span>参数


<span id="_______FileLockAddress______"></span><span id="_______filelockaddress______"></span><span id="_______FILELOCKADDRESS______"></span> *FileLockAddress*   
指定文件锁结构的十六进制地址。

<span id="_______ObjectAddress______"></span><span id="_______objectaddress______"></span><span id="_______OBJECTADDRESS______"></span> *ObjectAddress*   
指定拥有文件锁定的文件对象的十六进制地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关文件对象的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

 

 





