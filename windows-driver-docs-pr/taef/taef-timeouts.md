---
title: TAEF 超时
description: TAEF 超时
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 807b6503aa77397906ec9a6ff827ed21becdedf8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796393"
---
# <a name="taef-timeouts"></a>TAEF 超时


按以下格式指定 TAEF 超时： *\[ Day。 \]小时 \[ ：分钟 \[ ：秒 \[ 。\]FractionalSeconds \] 。 \]*

例如：

*0：0：0。5*  
指定5秒超时。

<span id="0_0_45"></span>*0:0:45*  
指定45秒超时。

<span id="0_20_or_0_20_0"></span><span id="0_20_OR_0_20_0"></span>*0:20* 或 *0:20:0*  
指定20分钟超时。

<span id="5_or_5_0_or_5_0_0"></span><span id="5_OR_5_0_OR_5_0_0"></span>*5* 或 *5:0* 或 *5:0:0*  
指定5小时超时。

<span id="1.2_or_1.2_0_or_1.2_0_0"></span><span id="1.2_OR_1.2_0_OR_1.2_0_0"></span>*1.2* 或 *1.2： 0* 或 *1.2：0： 0*  
指定1天和2小时超时。

## <a name="span-idsession_time-outsspanspan-idsession_time-outsspanspan-idsession_time-outsspansession-time-outs"></a><span id="Session_Time-outs"></span><span id="session_time-outs"></span><span id="SESSION_TIME-OUTS"></span>会话超时


当使用 **/sessionTimeout** 选项时，可以为 Te.exe 的整个执行指定会话超时。 如果超时时间已到，则测试会话将正常停止， [进程退出代码](exit-codes-for-taef.md) 将表示发生了超时。

<span id="te.exe_test1.dll__sessionTimeout_0_20"></span><span id="te.exe_test1.dll__sessiontimeout_0_20"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_20"></span>te.exe test1.dll/sessionTimeout：0：20  
整个测试会话将在20分钟后超时。

## <a name="span-idtest_time-outsspanspan-idtest_time-outsspanspan-idtest_time-outsspantest-time-outs"></a><span id="Test_Time-outs"></span><span id="test_time-outs"></span><span id="TEST_TIME-OUTS"></span>测试超时


可以通过将超时元数据应用于给定的测试程序集、类或方法来指定测试超时。

此外，当你使用/testTimeout 选项时，可在运行时重写超时元数据值。 如果指定，/testTimeout 将为 Te.exe 的整个执行设置全局测试超时。

**注意：** 当与 [/inproc](te-exe-command-line-parameters.md#inproc)结合使用时，将忽略测试超时。

<span id="te.exe_test1.dll__testTimeout_0_0_45"></span><span id="te.exe_test1.dll__testtimeout_0_0_45"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_0_45"></span>te.exe test1.dll/testTimeout：0：0：45  
每个测试和安装/清理方法将在45秒后超时。

 

 





