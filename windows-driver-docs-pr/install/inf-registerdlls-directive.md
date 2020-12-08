---
title: INF RegisterDlls 指令
description: RegisterDlls 指令引用一个或多个 INF 节，用于指定作为 OLE 控件并且需要自注册的文件。
keywords:
- INF RegisterDlls 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF RegisterDlls Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e8a15426474d25417724e6e3330cb24c3586b13
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831701"
---
# <a name="inf-registerdlls-directive"></a>INF RegisterDlls 指令


**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 可以使用 [Reg2inf 工具](../devtest/reg2inf.md) 将现有 [inf RegisterDlls 指令](../install/inf-registerdlls-directive.md) 转换为 [INF AddReg 指令](../install/inf-addreg-directive.md) ，以便将驱动程序包设置为通用。  有关详细信息，请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

**RegisterDlls** 指令引用一个或多个 INF 节，用于指定作为 OLE 控件并且需要自注册的文件。

```inf
[DDInstall]
  
RegisterDlls=register-dll-section[,register-dll-section]...
```

**RegisterDlls** 指令引用的每个 INF 部分都必须具有以下条目格式：

```inf
[register-dll-section] 
  
dirid,[subdir],filename,registration-flags[,[timeout][,argument]] 
```

*注册 dll 部分* 可以有任意数量的条目，每个条目都在单独的行中。

## <a name="entries"></a>项


<a href="" id="dirid"></a>*dirid*  
指定要注册的文件的目标目录 ID。 有关详细信息，请参阅 [Using Dirids](using-dirids.md)。

<a href="" id="subdir"></a>*subdir*  
指定要注册的文件的相对于当前目录的目录路径。 如果未指定，则文件位于当前目录中。

<a href="" id="filename"></a>*名字*  
标识要注册的 OLE 控件的文件名。

<a href="" id="registration-flags"></a>*注册标志*  
指示要对 OLE 控件执行的注册操作。 必须指定以下一个或两个标志。

<a href="" id="0x00000001--flg-regsvr-dllregister-"></a>**0x00000001** (FLG_REGSVR_DLLREGISTER)   
调用 OLE 控件的 **DllRegisterServer** 函数 (Windows SDK 文档) 中所述。

<a href="" id="0x00000002--flg-regsvr-dllinstall--"></a>**0x00000002** (FLG_REGSVR_DLLINSTALL)    
调用 OLE 控件的 **DllInstall** 函数 (Windows SDK 文档) 中所述。

<a href="" id="timeout"></a>*timeout*  
指定 OLE 控件完成指定注册调用的超时（以秒为单位）。 默认超时值为60秒。

<a href="" id="argument"></a>*实际*  
如果控件是可执行文件，则这是传递给可执行文件的命令字符串。 默认参数为 **/RegServer**。

如果控件不是可执行文件，则此参数指定要传递给 **DllInstall** 函数的命令行参数。

<a name="remarks"></a>备注
-------

对于 INF 文件，每个 *注册 dll 节* 名称必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

以下规则适用于用于设备安装的 **RegisterDlls** 指令：

-   尽管该语法允许 filename 为 DLL 或可执行文件，但对于设备安装，只允许使用一个 DLL。
-   要注册的代码不得提示用户输入。
-   服务器端安装在系统上下文中执行。 因此，您必须确保所注册的代码不包含任何安全漏洞，并且该文件权限会阻止恶意代码修改。

有关 OLE 控件和自行注册的详细信息，请参阅 Windows SDK 文档。

<a name="examples"></a>示例
--------

```inf
[Dialer]
RegisterDlls = DialerRegSvr
[DialerUninstall]
UnregisterDlls = DialerRegSvr
[DialerRegSvr]
11,,avtapi.dll, 1
```

## <a name="see-also"></a>另请参阅


[**UnregisterDlls**](inf-unregisterdlls-directive.md)

 

 






