---
title: 开发和测试工具
description: 开发和测试工具
ms.assetid: 6cc81509-27e1-4d5b-996c-6a7bbfd0ddcf
keywords:
- 筛选器管理器 WDK 文件系统微筛选器工具
- Fltmc.exe WDK 文件系统微筛选器
- fltkd 调试器扩展 WDK 文件系统微筛选器
- 筛选器验证程序 WDK 文件系统微筛选器
- 验证程序实用工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73737850d38bc3ddfb5e0f6fb38581e40d43fe10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522435"
---
# <a name="development-and-testing-tools"></a>开发和测试工具


在本部分中所述的筛选器管理器工具提供了 IFS 工具包的 Windows Server 2003 sp1 和中 Windows Driver Kit (WDK) 适用于 Windows Vista 及更高版本。

微筛选器驱动程序开发人员也是建议使用常规用途的内核模式下开发和测试工具，如 PREfast 使用特定于驱动程序的规则。

### <a name="span-idfltmcexecontrolprogramspanspan-idfltmcexecontrolprogramspanspan-idfltmcexecontrolprogramspanfltmcexe-control-program"></a><span id="Fltmc.exe_Control_Program"></span><span id="fltmc.exe_control_program"></span><span id="FLTMC.EXE_CONTROL_PROGRAM"></span>Fltmc.exe 控件程序

Fltmc.exe 控件程序是用于常见微筛选器驱动程序管理操作的命令行实用工具。 开发人员可以使用 Fltmc.exe 加载和卸载微筛选器驱动程序、 微筛选器驱动程序附加到卷或卷，从分离它们并枚举微筛选器驱动程序、 实例和卷。

### <a name="span-idfltkddebuggerextensionspanspan-idfltkddebuggerextensionspanspan-idfltkddebuggerextensionspanfltkd-debugger-extension"></a><span id="_fltkd_Debugger_Extension"></span><span id="_fltkd_debugger_extension"></span><span id="_FLTKD_DEBUGGER_EXTENSION"></span>！ fltkd 调试器扩展

！ 中提供 fltkd 调试器扩展[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)工具。 常用的命令如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>!cbd</strong></p></td>
<td align="left"><p>筛选器管理器等效于 ！ irp</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!filter</strong></p></td>
<td align="left"><p>列出有关指定的筛选器的详细的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!filters</strong></p></td>
<td align="left"><p>列出所有附加微筛选器驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!frames</strong></p></td>
<td align="left"><p>列表管理器框架的所有过滤器和附加微筛选器驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!instance</strong></p></td>
<td align="left"><p>列出有关的指定实例的详细的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!volume</strong></p></td>
<td align="left"><p>列出有关指定卷的详细的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!volumes</strong></p></td>
<td align="left"><p>列出所有卷并已附加微筛选器驱动程序实例</p></td>
</tr>
</tbody>
</table>

 

有关更多调试帮助测试微筛选器驱动程序通过 Fltmgr.sys，其中包含大量的 ASSERT 语句捕获常见错误的调试版本。

### <a name="span-idfilterverifierspanspan-idfilterverifierspanspan-idfilterverifierspanfilter-verifier"></a><span id="Filter_Verifier"></span><span id="filter_verifier"></span><span id="FILTER_VERIFIER"></span>筛选器验证工具

筛选器验证工具是[I/O 验证](https://msdn.microsoft.com/library/windows/hardware/ff548045)选项[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)验证微筛选器驱动程序使用的筛选器管理器函数。 使用筛选器管理器安装筛选器验证程序。 开发人员应始终开发微筛选器驱动程序与 Driver Verifier 和筛选器验证程序已启用。

若要使用筛选器验证器，指定微筛选器驱动程序的名称，并启用驱动程序验证程序 (Verifier.exe) 中的 I/O 验证选项。 验证开始时向筛选器管理器注册微筛选器驱动程序。

筛选器验证程序验证微筛选器驱动程序中的以下用法：

-   正确使用方法的参数和调用上下文

-   正确从 preoperation 和 postoperation 回调例程的返回值

-   统一且一致的更改到回调数据中的参数

筛选器验证工具跟踪以下筛选器管理器对象：

-   上下文

-   回调数据结构

-   排队的工作项

-   NameInformation 结构

-   File 对象

-   筛选器对象

-   实例对象

-   Volume 对象

 

 




