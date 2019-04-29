---
title: INF UnregisterDlls 指令
description: UnregisterDlls 指令引用用来指定 OLE 控件并需要自行注销 （自我删除） 的文件的一个或多个 INF 部分。
ms.assetid: 11d29c7f-9bd8-4097-9842-ce7431389241
keywords:
- INF UnregisterDlls 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF UnregisterDlls Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c015891175f687d8035116efa48e5a30e2e170a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325805"
---
# <a name="inf-unregisterdlls-directive"></a>INF UnregisterDlls 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**UnregisterDlls**指令引用用来指定 OLE 控件并需要自行注销 （自我删除） 的文件的一个或多个 INF 部分。

```ini
[DDInstall]
  
UnregisterDlls=unregister-dll-section[,unregister-dll-section]...
```

引用的每个 INF 部分**UnregisterDlls**指令必须具有以下条目格式：

```ini
[unregister-dll-section] 
  
dirid,[subdir],filename,registration-flags[,[timeout][,argument]] 
```

*撤消注册 dll 部分*可以有任意数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="dirid"></a>*dirid*  
指定要取消注册该文件的目标目录 ID。 有关详细信息，请参阅[使用 Dirids](using-dirids.md)。

<a href="" id="subdir"></a>*subdir*  
指定的目录路径，相对于当前目录中，要注销的文件。 如果未指定，该文件是当前目录中。

<a href="" id="filename"></a>*filename*  
标识要注销的 OLE 控件的文件名称。

<a href="" id="registration-flags"></a>*registration-flags*  
指示 OLE 控件上执行注册操作。 必须指定一个或两个以下的标志。

<a href="" id="0x00000001--flg-regsvr-dllregister-"></a>**0x00000001** (FLG_REGSVR_DLLREGISTER)  
调用**DllUnRegisterServer**函数 （Windows SDK 文档中所述）。

<a href="" id="0x00000002--flg-regsvr-dllinstall--"></a>**0x00000002** (FLG_REGSVR_DLLINSTALL)   
调用 OLE 控件的**DllInstall**函数 （Windows SDK 文档中所述）。

<a href="" id="timeout"></a>*timeout*  
指定超时，以秒为 OLE 控件才能完成指定的注销调用为单位。 默认超时值为 60 秒。

<a href="" id="argument"></a>*自变量*  
如果控件是可执行文件，这是传递给可执行文件的命令字符串。 默认自变量是 **/UnRegServer**。

如果控件不是可执行文件，此参数指定命令行参数来传递给**DllInstall**函数。

<a name="remarks"></a>备注
-------

每个*撤消注册 dll 部分*名称必须是唯一的 INF 文件和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

有关 OLE 控件和自注销的详细信息，请参阅 Windows SDK 文档。

<a name="examples"></a>示例
--------

```ini
[Dialer]
RegisterDlls = DialerRegSvr

[DialerUninstall]
UnregisterDlls = DialerRegSvr

[DialerRegSvr]
11,,avtapi.dll, 1
```

## <a name="see-also"></a>请参阅


[**RegisterDlls**](inf-registerdlls-directive.md)

 

 






