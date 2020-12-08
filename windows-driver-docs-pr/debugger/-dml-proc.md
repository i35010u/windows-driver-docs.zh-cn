---
title: dml_proc
description: Dml_proc 扩展显示进程的列表，并提供链接以获取有关进程的更详细信息。
keywords:
- dml_proc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dml_proc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b31c4bd4816644dd8586654b2c4de577fbf6d170
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805877"
---
# <a name="dml_proc"></a>！ dml \_ proc


**！ Dml \_ proc** extension 显示进程列表，并提供链接以获取有关进程的更详细信息。

```dbgcmd
!dml_proc
```

<a name="remarks"></a>备注
-------

下图显示了由 **！ dml \_ proc** 显示的输出的一部分。

![的屏幕截图！ dml \- proc 输出](images/dmlproc01.png)

在上面的输出中，进程地址是可单击以查看更多详细信息的链接。 例如，如果单击 " **fffffa80 \` 04e2b700** " (mobsync.exe) 的地址，则会看到有关 mobsync.exe 过程的详细信息，如下图所示。

![进程详细信息的屏幕截图](images/dmlproc02.png)

前面的输出描述单个进程，其中包含的链接可用于更详细地浏览进程及其线程。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[调试器标记语言命令](debugger-markup-language-commands.md)

 

 






