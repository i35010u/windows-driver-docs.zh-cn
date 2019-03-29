---
title: TAEF 超时
description: TAEF 超时
ms.assetid: 43FE81A2-71DF-4e3a-998E-1B1F8C1398AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b4aa6ed9f767e57cfeff6c1f2a65d76c00febb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575920"
---
# <a name="taef-timeouts"></a>TAEF 超时


按以下格式指定 TAEF 超时值：*\[某一天。\]小时\[： 分钟\[： 第二个\[。秒的小数部分\]\]\]*。

例如：

*0:0:0.5*  
指定.5 的第二个超时值。

<span id="0_0_45"></span>*0:0:45*  
指定 45 秒超时值。

<span id="0_20_or_0_20_0"></span><span id="0_20_OR_0_20_0"></span>*0:20*或*0:20:0*  
指定 20 分钟的超时时间。

<span id="5_or_5_0_or_5_0_0"></span><span id="5_OR_5_0_OR_5_0_0"></span>*5*或*5:0*或*5:0:0*  
指定 5 小时超时值。

<span id="1.2_or_1.2_0_or_1.2_0_0"></span><span id="1.2_OR_1.2_0_OR_1.2_0_0"></span>*1.2*或*1.2:0*或*1.2:0:0*  
指定 1 天、 每天 2 个小时超时值。

## <a name="span-idsessiontime-outsspanspan-idsessiontime-outsspanspan-idsessiontime-outsspansession-time-outs"></a><span id="Session_Time-outs"></span><span id="session_time-outs"></span><span id="SESSION_TIME-OUTS"></span>会话超时值


在使用时，可以 Te.exe 的整个执行指定会话超时 **/sessionTimeout**选项。 如果在超时到期，将正常停止测试会话，并[处理退出代码](exit-codes-for-taef.md)将表示出现超时。

<span id="te.exe_test1.dll__sessionTimeout_0_20"></span><span id="te.exe_test1.dll__sessiontimeout_0_20"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_20"></span>te.exe test1.dll /sessionTimeout:0:20  
在整个测试会话会在 20 分钟后超时。

## <a name="span-idtesttime-outsspanspan-idtesttime-outsspanspan-idtesttime-outsspantest-time-outs"></a><span id="Test_Time-outs"></span><span id="test_time-outs"></span><span id="TEST_TIME-OUTS"></span>测试超时值


可以通过将超时元数据应用于给定的测试程序集、 类或方法指定测试超时值。

此外，如果使用 /testTimeout 选项在运行时重写超时元数据值。 如果指定，/testTimeout 设置 Te.exe 整个执行的全球化测试超时值。

**注意：** 结合使用时，将忽略测试超时值[/inproc](te-exe-command-line-parameters.md#inproc)。

<span id="te.exe_test1.dll__testTimeout_0_0_45"></span><span id="te.exe_test1.dll__testtimeout_0_0_45"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_0_45"></span>te.exe test1.dll /testTimeout:0:0:45  
每个测试和安装程序/清理方法将在 45 秒后超时。

 

 





