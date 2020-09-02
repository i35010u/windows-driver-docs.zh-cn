---
title: PwrTest 语法
description: 在命令提示符窗口中运行 PwrTest。 您可以使用命令选项来选择和配置 PwrTest 方案。
ms.assetid: bcae1bb6-ce5b-4ece-a5ba-bae6fefd6408
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9332707c8790f5a09e545bfe35809aaf133213d0
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381937"
---
# <a name="pwrtest-syntax"></a>PwrTest 语法


在命令提示符窗口中运行 PwrTest。 您可以使用命令选项来选择和配置 [PwrTest 方案](pwrtest-scenarios.md) 。

PwrTest 工具的语法为：

```
pwrtest /scenario [/scenario_options] [/common_options]
```

<span id="_scenario"></span><span id="_SCENARIO"></span>**/**<em>应用</em>  

| 方案   | 说明                                                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| sleep       | 通过睡眠/恢复转换循环计算机。  (Windows 7 及更高版本)                                                                                         |
| 电池     | 提供电池信息和监视。  (Windows 7 及更高版本)                                                                                                  |
| info        | 提供系统电源信息。  (Windows 7 及更高版本)                                                                                                            |
| es          | 监视线程执行状态。  (Windows 7 及更高版本)                                                                                                              |
| 空闲        | 监视系统空闲事件。  (Windows 7 及更高版本)                                                                                                                  |
| 黑白         | 监视处理器电源管理。  (Windows 7 及更高版本)                                                                                                          |
| 计时器       | 监视系统计时器分辨率更改。  (Windows 7 及更高版本)                                                                                                     |
| disk        | 监视磁盘空闲统计信息和降速事件。  (Windows 7 及更高版本)                                                                                           |
| 设备      | 监视设备空闲统计信息和电源关闭事件。  (Windows 7 及更高版本)                                                                                        |
| 监视     | 记录与监视器/显示自动变暗和消隐相关的用户空闲统计信息。 (Windows 7 及更高版本)                                                             |
| 请求    | 显示未完成和新的电源请求。  (Windows 7 及更高版本)                                                                                                  |
| 散热     | 监视 ACPI 热量区域信息和统计信息。 这仅在报告热量区域和温度变化的系统上受支持。  (Windows 7 及更高版本) 。 |
| processidle | 强制后台维护任务立即执行 (，而不是在计划时间) 执行，并监视其进度。  (Windows 7 及更高版本)                         |
| cs          | 如果系统支持计算机，则通过连接的备用转换来循环计算机。  (Windows 8 及更高版本)                                                |
| platidle    | 监视和尝试记录平台空闲转换计数（如果系统支持）。  (Windows 8 及更高版本)                                             |
| directedfx  | 监视与 [定向电源管理框架 (DFx) ](../kernel/introduction-to-the-directed-power-management-framework.md)相关的低功耗空闲状态开关。  (Windows 10 版本1903及更高版本) |


 


<span id="_scenario_options"></span><span id="_SCENARIO_OPTIONS"></span>**/**<em>方案 \_ 选项</em>  
若要查看每个 Pwrtest 方案的可用选项，请键入： **pwrtest.exe/**<em>方案</em> **/？**

例如： **pwrtest.exe/sleep/？**

<span id="_common_options"></span><span id="_COMMON_OPTIONS"></span>/*常用 \_ 选项*  

|       *常用 \_ 选项*       |                                                                                                                说明                                                                                                                 |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    **/lf：**<em>文件夹</em>    |                                            指定日志文件的文件夹。 例如，c： \\ myfolder 或 \\ \\ 服务器 \\ 共享。 默认的日志位置与 pwrtest.exe 的文件夹相同。                                             |
|     **/ln：**<em>名称</em>     |                指定日志文件的名称以及 Windows (ETW) trace 会话的事件跟踪的名称。 日志文件扩展名会自动添加 ( wtl、.xml 等 ) 。 默认名称为 pwrtestlog。                |
| **/etwbuffersize：**<em>n</em> |                                                  指定 ETW 缓冲区大小（以 KB 为单位）（如果大于默认大小）。 默认值为当前页大小或 256KB (，取两者中的较大) 。                                                  |
| **/etwminbuffers：**<em>n</em> |                                如果大于每个逻辑处理器2的最小值，则指定为 ETW 会话分配的最小缓冲区数。 默认值为每个逻辑处理器2个缓冲区。                                |
| **/etwmaxbuffers：**<em>n</em> | 指定为 ETW 会话分配的最大缓冲区数（如果该数目大于每个逻辑处理器2的最小值，而大于 **etwminbuffers** 设置）。 默认值为 **etwminbuffers** 值 + 20。 |
|        **/delaywrite**        |                                                           指定在内存中缓存日志数据以减少磁盘写入量。 此选项会影响包含 ETL 的所有日志类型。                                                            |

**示例**

```
pwrtest /?  
```

```
pwrtest /requests  /?
```

```
pwrtest /requests  /t:60
```

### <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注

支持 ETW 跟踪的执行要求：

-   Pwrtest 必须从管理员或提升的 **命令提示符** 窗口中运行 (**以管理员) 运行** 。

-   Pwrtest 必须以本机方式运行 (WoW64 不支持) 。

系统管理员所放置的组策略设置可能会干扰一些需要暂时修改电源设置值 (如睡眠方案) 的方案。

PwrTest 会在中为每个执行自动生成多个日志。日志 (纯文本) ，.xml (格式因应用场景而异) ，. wtl (WTTLog) 和 .etl (ETW 跟踪) 日志格式。

为了能够使用所有 PwrTest 方案，你必须首先设置测试计算机，以便使用 Visual Studio 和 WDK 进行测试。 有关详细信息，请参阅 [设置计算机以进行驱动程序部署和测试 (wdk 8.1) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)，或 [预配用于驱动程序部署和测试 (WDK 8) ](/previous-versions/hh698272(v=vs.85))的计算机。 某些方案需要电源按钮驱动程序，该驱动程序是 Windows 驱动程序测试框架的一部分 (WDTF) 。 使用 Visual Studio 和 WDK 预配系统进行测试时，会自动安装 WDTF (和随附的电源按钮驱动程序) 。 有关 WDTF 的信息，请参阅 [**Windows 设备测试框架 (WDTF)  (Windows 驱动程序) **](../wdtf/index.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 方案](pwrtest-scenarios.md)

[PwrTest 日志文件](pwrtest-log-file.md)

 

