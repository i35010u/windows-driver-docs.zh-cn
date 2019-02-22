---
title: dml_proc
description: Dml_proc 扩展显示的进程的列表，并提供用于获取进程的更多详细的信息的链接。
ms.assetid: 35B5B2E7-07CE-4F44-819D-9B7C76273F9A
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
ms.openlocfilehash: b95722679652d383f221ce59db5126829ba42edf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526806"
---
# <a name="dmlproc"></a>!dml\_proc


**！ Dml\_proc**扩展显示的进程的列表，并提供用于获取进程的更多详细的信息的链接。

```dbgcmd
!dml_proc
```

<a name="remarks"></a>备注
-------

下图显示了一部分显示的输出 **！ dml\_proc**。

![屏幕截图: ！ dml\-proc 输出](images/dmlproc01.png)

在上面的输出中，进程地址是你可以单击以查看更多详细的信息的链接。 例如，如果您单击**fffffa80\`04e2b700** （mobsync.exe 的地址），将看到有关 mobsync.exe 过程的详细的信息，如在下图中所示。

![进程详细信息的屏幕截图](images/dmlproc02.png)

上面的输出，其中描述了单个进程，包含可单击来浏览进程和线程中更多详细信息的链接。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[调试器标记语言命令](debugger-markup-language-commands.md)

 

 






